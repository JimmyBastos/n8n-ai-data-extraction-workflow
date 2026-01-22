# Live Truck Availability Extraction Workflow

An n8n workflow that automatically extracts structured data from carrier emails about truck availability using LLM-powered extraction with hallucination detection and correction.

## Introduction

Carriers frequently send emails to share truck locations and availability dates. These "live truck" emails vary widely in format, detail, and writing style—from formal structured lists to brief informal messages.

This workflow automates the extraction of structured logistics data from these emails, including:
- Carrier identification (MC number, company name)
- Equipment type (van, reefer, flatbed)
- Availability dates
- Origin locations
- Destination preferences
- Multiple truck extraction - Handles emails with multiple truck availabilities in a single message
- Confidence scoring and human review flagging

## Approach

The workflow implements a **two-pass extraction strategy** with hallucination detection:

1. **Initial Extraction**: An LLM extracts structured data from the email using a detailed prompt with industry-specific guidance and JSON schema constraints.

2. **Validation**: JavaScript code validates required fields and adjusts confidence scores based on data completeness.

3. **Inference Detection**: A custom algorithm checks if extracted values actually appear in the source email, flagging potential hallucinations.

4. **Correction Pass**: If inferences are detected, a second LLM call corrects hallucinated values by cross-referencing against the original email.

5. **Human Review Routing**: Low-confidence or incomplete extractions are flagged for human review.

### Key Design Decisions

- **Explicit data over inference**: The prompt instructs the model to only extract data that explicitly appears in the email, with minimal normalization allowed for industry-standard abbreviations.
- **Raw text preservation**: Original text is always stored alongside normalized values for auditability.
- **Confidence-based routing**: Extractions scoring below 0.7 confidence automatically require human review.
- **Retry on failure**: LLM nodes have built-in retry logic for transient failures.

## Tools & Models

### Platform
- **n8n** - Workflow automation platform

### LLM Models
- **GPT-4.1-mini** - Initial extraction (fast, strong inference)
- **GPT-4.1-nano** - Correction pass (fast, cost-effective)
- **GPT-5-nano** - Discarded (reasoning capabilities caused over-correction, removing valid inferred data)

## Getting Started

### Prerequisites
- n8n instance (self-hosted or cloud)
- OpenAI API key

### Installation

1. **Import the workflow**
   - Open n8n
   - Go to **Workflows** → **Import from File**
   - Select `workflow.json`

2. **Configure OpenAI credentials**
   - Go to **Settings** → **Credentials**
   - Click **Add Credential** → **OpenAI API**
   - Enter your API key ([Get one here](https://platform.openai.com/api-keys))
   - Save and link to the workflow's OpenAI nodes

3. **Activate the workflow**
   - Toggle the workflow to **Active**
   - Note the webhook URL displayed
   

## Testing

### Webhook Endpoint

```
POST /webhook/extractors/a86054b3-6ea0-4267-84d6-3180203e026e/emails
```

### Request Format

```json
{
  "messageId": "unique-message-id",
  "from": "carrier@example.com",
  "to": "dispatch@example.com",
  "date": "2026-01-13T10:00:00Z",
  "Subject": "Truck Availability",
  "text": "Email body content here"
}
```

### Using cURL

```bash
curl -X POST "https://your-n8n-instance/webhook/extractions/d19cbcdc-d8a9-465a-af00-5f27531aca1d/trucks" \
  -H "Content-Type: application/json" \
  -d '{
    "messageId": "test-001",
    "from": "carrier@trucking.com",
    "to": "dispatch@company.com",
    "date": "2026-01-13T10:00:00Z",
    "Subject": "Truck Available",
    "text": "Have a 53 van empty Monday in Chicago heading to Dallas."
  }'
```

## Request Samples

See [SAMPLES.md](SAMPLES.md) for complete input/output examples:

| Sample | Description | Trucks | Review Required |
|--------|-------------|--------|----------------|
| [1. Structured Multi-Truck](SAMPLES.md#1-structured-multi-truck-list) | Multiple trucks from various origins to Columbus | 7 | Yes (missing equipment) |
| [2. Daily Schedule](SAMPLES.md#2-daily-schedule-with-equipment-types) | Weekly availability with specific equipment types | 8 | Yes (missing MC#) |
| [3. Simple One-Liner](SAMPLES.md#3-simple-one-liner) | Brief informal message with minimal details | 1 | Yes (inferred state) |
| [4. Informal No Punctuation](SAMPLES.md#4-informal-no-punctuation) | Short message without formatting | 1 | Yes (inferred states) |
| [5. Contact Info](SAMPLES.md#5-with-contact-info) | Vague availability with phone number | 1 | Yes (incomplete data) |
| [6. Regional Destination](SAMPLES.md#6-regional-destination) | Generic regional destination preference | 1 | Yes (inferred state) |
| [7. Minimal Details](SAMPLES.md#7-minimal--no-details) | Almost no usable information | 1 | Yes (low confidence) |

## Assumptions

1. **Multiple trucks supported**: The workflow now extracts multiple truck availabilities from a single email, with per-truck metadata and validation.

2. **Date resolution**: Relative dates (e.g., "tomorrow", "Monday") are resolved using the email's sent date as the anchor.

3. **US geography focus**: Location normalization assumes US cities and states.

4. **Equipment categories**: Limited to `van`, `reefer`, `flatbed`, `unknown`, and `other`.

### Node Descriptions

| Node | Type | Purpose |
|------|------|---------|
| **Webhook** | Trigger | Receives incoming email data via HTTP POST |
| **EmailData** | Set | Normalizes input fields (messageId, from, to, date, subject, text) |
| **ParsedEmail** | Markdown | Converts HTML email content to clean text |
| **DataExtractionModel** | OpenAI | First-pass LLM extraction with JSON schema |
| **ExtractionOutput** | Set | Extracts JSON from LLM response |
| **DataValidation** | Code | Validates required fields, adjusts confidence |
| **InferenceCheck** | Code | Detects hallucinated/inferred values |
| **IfHasInferredData** | If | Routes based on inference detection |
| **DataCorrectionModel** | OpenAI | Second-pass LLM to correct hallucinations |
| **CorrectionOutput** | Set | Extracts corrected JSON |
| **IfRequireHumanReview** | If | Routes based on review requirements |
| **Respond to Webhook** | Response | Returns final JSON response |


## Data Validation and Quality Control

The workflow implements comprehensive validation and hallucination detection to ensure data quality:

### Validation Logic

After extraction, each truck entry is validated for required fields and confidence thresholds. The validation checks both individual truck records and root-level carrier information.

**Required fields per truck:**
- Equipment category
- Availability date
- Origin city and state

**Root-level requirements:**
- Carrier MC number

**Review triggers:**
- Missing any required fields → `incomplete_core_fields` flag
- Confidence score below 0.7 → `low_confidence_score` flag
- Any truck requiring review escalates the entire extraction to human review

### Inference Detection

The workflow detects hallucinated or inferred data by verifying that extracted values actually appear in the source email text. This prevents the LLM from inferring information that isn't explicitly stated.

**How it works:**
1. Every string value in the extraction is compared against the original email text using case-insensitive substring matching
2. Values that don't appear in the email are flagged as inferred
3. Inferred fields are logged in `metadata.inferences.fields` with their full path
4. Safe fields that are allowed to be inferred (like `sourceType`, `date`, `category`) are excluded from checking

**Example:**
- Email: `"Have a van empty Monday in Chicago"`
- Extracted: `origin.state = "IL"`
- Result: Flagged as inferred because "IL" doesn't appear in the email text

### Correction Pass

When inferred fields are detected, a second LLM call is triggered to correct the extraction:
- The correction model cross-references all extracted values against the original email
- Values that aren't explicitly stated are removed or set to null
- Only data that appears in the source text is preserved

This two-pass approach significantly reduces hallucinations while maintaining extraction quality.


## Future Improvements
- Integration with a carrier database for MC number validation
- Batch processing endpoint for high-volume scenarios
- Webhook authentication/API key support
- Configurable confidence thresholds
- Support for attachments (spreadsheets, images)
- Enhanced date parsing for ambiguous relative dates
- Multi-language support beyond English
