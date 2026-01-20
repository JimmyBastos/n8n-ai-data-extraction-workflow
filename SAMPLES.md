# Request Samples

## 1. Complete Email (High Confidence)

**Input:**
```json
{
  "messageId": "sample-001",
  "from": "dispatch@carrierco.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T09:00:00Z",
  "Subject": "Truck Availability - MC# 224990",
  "text": "Hello!\n\nLooking to move the trucks below towards Columbus, OH.\n\nMC# 224990\n\nTUESDAY 01-20\nPITTSBURGH PA - 53' DRY VAN\n\nTO: Louisville KY, Cleveland OH, Lexington KY"
}
```

**Expected Output:**
```json
{
	"carrier": {
		"mcNumber": "224990",
		"companyName": null
	},
	"truckAvailability": {
		"equipment": {
			"category": "van",
			"configuration": "53' DRY VAN",
			"features": null
		},
		"availability": {
			"date": "2026-01-20",
			"dateRaw": "TUESDAY 01-20"
		},
		"origin": {
			"city": "Pittsburgh",
			"state": "PA",
			"rawText": "PITTSBURGH PA"
		},
		"destinationPreference": {
			"type": "region",
			"region": "Cleveland OH",
			"city": null,
			"state": null
		},
		"notes": null
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.9,
			"requiresHumanReview": false,
			"reviewReasons": []
		},
		"inferences": {
			"fields": []
		}
	}
}
```

---

## 2. Short or Informal Email (with typo)

**Input:**
```json
{
  "messageId": "sample-002",
  "from": "driver@gmail.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T14:30:00Z",
  "Subject": "truck",
  "text": "reefer open tomorrow atlanta - CA heading southeast"
}
```

**Expected Output:**
```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"truckAvailability": {
		"equipment": {
			"category": "reefer",
			"configuration": null,
			"features": null
		},
		"availability": {
			"date": "2026-01-20",
			"dateRaw": "tomorrow"
		},
		"origin": {
			"city": "Atlanta",
			"state": "GA",
			"rawText": "atlanta - CA"
		},
		"destinationPreference": {
			"type": "region",
			"region": "Southeast",
			"city": null,
			"state": null
		},
		"notes": null
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.74,
			"requiresHumanReview": true,
			"reviewReasons": [
				"ambiguous_data",
			]
		},
		"inferences": {
			"fields": [
				"truckAvailability.origin.state"
			],
			"severity": "medium"
		}
	}
}
```

---

## 3. Missing or Unclear Details

**Input:**
```json
{
  "messageId": "sample-003",
  "from": "unknown@carrier.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T08:00:00Z",
  "Subject": "availability",
  "text": "flatbed available next week, call me 555-222-3333"
}
```

**Expected Output:**
```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"truckAvailability": {
		"equipment": {
			"category": "flatbed",
			"configuration": null,
			"features": null
		},
		"availability": {
			"date": "2026-01-26",
			"dateRaw": "next week"
		},
		"origin": {
			"city": null,
			"state": null,
			"rawText": null
		},
		"destinationPreference": {
			"type": null,
			"region": null,
			"city": null,
			"state": null
		},
		"notes": [
			"call me 555-222-3333"
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.6,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields"
			]
		},
		"inferences": {
			"fields": []
		}
	}
}
```

---

## 4. Requires Human Follow-up

**Input:**
```json
{
  "messageId": "sample-004",
  "from": "info@trucking.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T16:00:00Z",
  "Subject": "capacity",
  "text": "Have capacity."
}
```

**Expected Output:**
```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"truckAvailability": {
		"equipment": {
			"category": null,
			"configuration": null,
			"features": null
		},
		"availability": {
			"date": null,
			"dateRaw": null
		},
		"origin": {
			"city": null,
			"state": null,
			"rawText": null
		},
		"destinationPreference": {
			"type": null,
			"region": null,
			"city": null,
			"state": null
		},
		"notes": [
			"Have capacity."
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.2,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields"
			]
		},
		"inferences": {
			"fields": []
		}
	}
}
```

---

## 5. Detailed Multi-Truck Email

**Input:**
```json
{
  "messageId": "sample-005",
  "from": "dispatch@megacarrier.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T07:00:00Z",
  "Subject": "Weekly Availability",
  "text": "01/20/2026- TUESDAY\nHARRISBURG, PA -53' VAN TEAM & SOLO DRIVERS- TO KANSAS CITY, KS\nBENSALEM, PA -53' VAN TO KANSAS CITY,KS\nHOUSTON, TX - 53' REEFER TO KANSAS CITY, KS"
}
```

**Expected Output:**
```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"truckAvailability": {
		"equipment": {
			"category": "van",
			"configuration": "53' VAN",
			"features": null
		},
		"availability": {
			"date": "2026-01-20",
			"dateRaw": "01/20/2026- TUESDAY"
		},
		"origin": {
			"city": "Harrisburg",
			"state": "PA",
			"rawText": "HARRISBURG, PA"
		},
		"destinationPreference": {
			"type": "city",
			"region": null,
			"city": "Kansas City",
			"state": "KS"
		},
		"notes": [
			"TEAM & SOLO DRIVERS"
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.8,
			"requiresHumanReview": true,
			"reviewReasons": [
				"multiple_entities_detected"
			]
		},
		"inferences": {
			"fields": []
		}
	}
}
```
