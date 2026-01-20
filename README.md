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
curl -X POST "https://your-n8n-instance/webhook/extractors/a86054b3-6ea0-4267-84d6-3180203e026e/emails" \
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

| Sample | Description | Confidence |
|--------|-------------|------------|
| [1. Complete Email](SAMPLES.md#1-complete-email-high-confidence) | Full details with MC#, location, equipment | 0.9 |
| [2. Short/Informal](SAMPLES.md#2-short-or-informal-email) | Brief message with minimal formatting | 0.74 |
| [3. Missing Details](SAMPLES.md#3-missing-or-unclear-details) | Incomplete data, no location | 0.6 |
| [4. Human Follow-up](SAMPLES.md#4-requires-human-follow-up) | Vague message requiring review | 0.2 |
| [5. Multi-Truck](SAMPLES.md#5-detailed-multi-truck-email) | Multiple availabilities in one email | 0.8 |

## Assumptions

1. **Single truck per extraction**: The workflow extracts one truck availability per email. Multi-truck emails flag `multiple_entities_detected` for human review.

2. **Date resolution**: Relative dates (e.g., "tomorrow", "Monday") are resolved using the email's sent date as the anchor.

3. **US geography focus**: Location normalization assumes US cities and states.

4. **Equipment categories**: Limited to `van`, `reefer`, `flatbed`, and `other`.

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

## Future Improvements

- Support for extracting multiple truck availabilities from a single email
- Integration with a carrier database for MC number validation
- Batch processing endpoint for high-volume scenarios
- Webhook authentication/API key support
- Configurable confidence thresholds
- Support for attachments (spreadsheets, images)
