# Email Test Samples

This file contains examples of truck availability emails and their expected extraction outputs. Each sample demonstrates different email formats and data quality scenarios.

**How to use:** Click on "Output Sample" to expand/collapse the JSON results.

---

## 1. Structured Multi-Truck List

**Input:**
```json
{
  "messageId": "sample-001",
  "from": "dispatch@carrierco.com",
  "to": "loads@broker.com",
  "date": "2026-01-13T09:00:00Z",
  "subject": "Truck Availability - MC# 224990",
  "text": "Hello!\n\nLooking to move the trucks below towards Columbus, OH. Please let us know if you have anything that matches up.\n\nMC# 224990\n\n|          TUESDAY 01-13          |\n|---------------------------------|\n| PITTSBURGH PA X4                |\n| BURLINGTON KY                   |\n| LOUISVILLE KY                   |\n| LIBERTY TWP OH                  |\n| SHEPHERDSVILLE KY               |\n| SPRINGVILLE IN                  |\n| CRANBERRY TWP PA                |\n| COLUMBUS TO: Louisville KY,     |\n| Pittsburgh PA, Cleveland OH,    |\n| Lexington KY, Toledo OH         |"
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": "224990",
		"companyName": null
	},
	"contact": null,
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "Hello!\n\nLooking to move the trucks below towards Columbus, OH. Please let us know if you have anything that matches up.\n\nMC# 224990\n\n|          TUESDAY 01-13          |\n|---------------------------------|\n| PITTSBURGH PA X4                |\n| BURLINGTON KY                   |\n| LOUISVILLE KY                   |\n| LIBERTY TWP OH                  |\n| SHEPHERDSVILLE KY               |\n| SPRINGVILLE IN                  |\n| CRANBERRY TWP PA                |\n| COLUMBUS TO: Louisville KY,     |\n| Pittsburgh PA, Cleveland OH,    |\n| Lexington KY, Toledo OH         |",
		"trucks": [
			{
				"truckCount": 4,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Pittsburgh",
					"state": "PA",
					"rawText": "PITTSBURGH PA"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Burlington",
					"state": "KY",
					"rawText": "BURLINGTON KY"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Louisville",
					"state": "KY",
					"rawText": "LOUISVILLE KY"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Liberty Twp",
					"state": "OH",
					"rawText": "LIBERTY TWP OH"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Shepherdsville",
					"state": "KY",
					"rawText": "SHEPHERDSVILLE KY"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Springville",
					"state": "IN",
					"rawText": "SPRINGVILLE IN"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-13",
					"dateRaw": "TUESDAY 01-13"
				},
				"origin": {
					"city": "Cranberry Twp",
					"state": "PA",
					"rawText": "CRANBERRY TWP PA"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Columbus, OH",
					"primaryCity": "Columbus",
					"primaryState": "OH",
					"acceptableDestinations": [
						{
							"city": "Louisville",
							"state": "KY"
						},
						{
							"city": "Pittsburgh",
							"state": "PA"
						},
						{
							"city": "Cleveland",
							"state": "OH"
						},
						{
							"city": "Lexington",
							"state": "KY"
						},
						{
							"city": "Toledo",
							"state": "OH"
						}
					],
					"rawText": "COLUMBUS TO: Louisville KY,     Pittsburgh PA, Cleveland OH,    Lexington KY, Toledo OH"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.75,
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

</details>

---

## 2. Daily Schedule with Equipment Types

**Input:**
```json
{
  "messageId": "sample-002",
  "from": "ops@freightlines.com",
  "to": "loads@broker.com",
  "date": "2026-01-09T08:30:00Z",
  "subject": "Weekly Availability",
  "text": "1/10 -SATURDAY\nOLNEY, IL - 53' REEFER TO KANSAS CITY, KS\n\n01/12/2026- MONDAY\nHARRISBURG, PA -53' VAN TEAM & SOLO DRIVERS- TO KANSAS CITY, KS\nBENSALEM, PA -53' VAN TO KANSAS CITY,KS\nELIZABETHTOWN, PA - 53' VAN AND REEFER TO KANSAS CITY, KS\nMOOSIC, PA -53' VAN TO KANSAS CITY, KS\nHOUSTON, TX - 53' REEFER TO KANSAS CITY, KS\nBURLINGTON, NC - 53' REEFER TO KANSAS CITY, KS"
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"contact": null,
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "1/10 -SATURDAY\nOLNEY, IL - 53' REEFER TO KANSAS CITY, KS\n\n01/12/2026- MONDAY\nHARRISBURG, PA -53' VAN TEAM & SOLO DRIVERS- TO KANSAS CITY, KS\nBENSALEM, PA -53' VAN TO KANSAS CITY,KS\nELIZABETHTOWN, PA - 53' VAN AND REEFER TO KANSAS CITY, KS\nMOOSIC, PA -53' VAN TO KANSAS CITY, KS\nHOUSTON, TX - 53' REEFER TO KANSAS CITY, KS\nBURLINGTON, NC - 53' REEFER TO KANSAS CITY, KS",
		"trucks": [
			{
				"truckCount": 1,
				"equipment": {
					"category": "reefer",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-10",
					"dateRaw": "1/10 -SATURDAY"
				},
				"origin": {
					"city": "Olney",
					"state": "IL",
					"rawText": "OLNEY, IL"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.9,
					"requiresHumanReview": false,
					"reviewReasons": []
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "van",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Harrisburg",
					"state": "PA",
					"rawText": "HARRISBURG, PA"
				},
				"driverType": [
					"team",
					"solo"
				],
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.9,
					"requiresHumanReview": false,
					"reviewReasons": []
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "van",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Bensalem",
					"state": "PA",
					"rawText": "BENSALEM, PA"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY,KS"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.9,
					"requiresHumanReview": false,
					"reviewReasons": []
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "van",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Elizabethtown",
					"state": "PA",
					"rawText": "ELIZABETHTOWN, PA"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": [
					"AND REEFER"
				],
				"metadata": {
					"confidenceScore": 0.8,
					"requiresHumanReview": true,
					"reviewReasons": [
						"ambiguous_data"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "reefer",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Elizabethtown",
					"state": "PA",
					"rawText": "ELIZABETHTOWN, PA"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": [
					"AND VAN"
				],
				"metadata": {
					"confidenceScore": 0.8,
					"requiresHumanReview": true,
					"reviewReasons": [
						"ambiguous_data"
					]
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "van",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Moosic",
					"state": "PA",
					"rawText": "MOOSIC, PA"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.9,
					"requiresHumanReview": false,
					"reviewReasons": []
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "reefer",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Houston",
					"state": "TX",
					"rawText": "HOUSTON, TX"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.9,
					"requiresHumanReview": false,
					"reviewReasons": []
				}
			},
			{
				"truckCount": 1,
				"equipment": {
					"category": "reefer",
					"configuration": "53'",
					"features": []
				},
				"availability": {
					"date": "2026-01-12",
					"dateRaw": "01/12/2026- MONDAY"
				},
				"origin": {
					"city": "Burlington",
					"state": "NC",
					"rawText": "BURLINGTON, NC"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "exact",
					"region": null,
					"primaryCity": "Kansas City",
					"primaryState": "KS",
					"acceptableDestinations": null,
					"rawText": "TO KANSAS CITY, KS"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.9,
					"requiresHumanReview": false,
					"reviewReasons": []
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.9,
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

</details>

---

## 3. Simple One-Liner

**Input:**
```json
{
  "messageId": "sample-003",
  "from": "driver@carrier.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T14:22:00Z",
  "subject": "Truck",
  "text": "Have a van empty Monday in Chicago."
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"contact": null,
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "Have a van empty Monday in Chicago.",
		"trucks": [
			{
				"truckCount": 1,
				"equipment": {
					"category": "van",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-20",
					"dateRaw": "Monday"
				},
				"origin": {
					"city": "Chicago",
					"state": "IL",
					"rawText": "Chicago"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "unspecified",
					"region": null,
					"primaryCity": null,
					"primaryState": null,
					"acceptableDestinations": null,
					"rawText": null
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.8,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.8,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields",
				"hallucination_corrected"
			]
		},
		"inferences": {
			"fields": [
				"availabilityBatch.trucks.0.origin.state"
			],
			"severity": "high"
		}
	}
}
```

</details>

---

## 4. Informal No Punctuation

**Input:**
```json
{
  "messageId": "sample-004",
  "from": "mike@fleet.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T11:05:00Z",
  "subject": "reefer",
  "text": "reefer open tomorrow atlanta heading southeast"
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"contact": null,
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "reefer open tomorrow atlanta heading southeast",
		"trucks": [
			{
				"truckCount": 1,
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
					"rawText": "atlanta"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "directional",
					"region": null,
					"primaryCity": "Atlanta",
					"primaryState": "GA",
					"acceptableDestinations": null,
					"rawText": "heading southeast"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.75,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields"
			]
		},
		"inferences": {
			"fields": [
				"availabilityBatch.trucks.0.origin.state",
				"availabilityBatch.trucks.0.destinationPreference.primaryState"
			],
			"severity": "medium"
		}
	}
}
```

</details>

---

## 5. With Contact Info

**Input:**
```json
{
  "messageId": "sample-005",
  "from": "joe@trucking.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T16:45:00Z",
  "subject": "Flatbed",
  "text": "flatbed available next week, call me 555-222-3333"
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"contact": {
		"phone": "555-222-3333",
		"email": null,
		"rawText": "call me 555-222-3333"
	},
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "flatbed available next week, call me 555-222-3333",
		"trucks": [
			{
				"truckCount": 1,
				"equipment": {
					"category": "flatbed",
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": null,
					"dateRaw": "next week"
				},
				"origin": {
					"city": null,
					"state": null,
					"rawText": null
				},
				"driverType": null,
				"destinationPreference": {
					"type": "unspecified",
					"region": null,
					"primaryCity": null,
					"primaryState": null,
					"acceptableDestinations": null,
					"rawText": null
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.5,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields",
						"ambiguous_data",
						"low_confidence_score"
					]
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.5,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields",
				"ambiguous_data",
				"low_confidence_score"
			]
		},
		"inferences": {
			"fields": []
		}
	}
}
```

</details>

---

## 6. Regional Destination

**Input:**
```json
{
  "messageId": "sample-006",
  "from": "dispatch@freight.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T10:00:00Z",
  "subject": "Friday",
  "text": "Truck opens Friday in Dallas looking Midwest"
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"contact": null,
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "Truck opens Friday in Dallas looking Midwest",
		"trucks": [
			{
				"truckCount": 1,
				"equipment": {
					"category": null,
					"configuration": null,
					"features": null
				},
				"availability": {
					"date": "2026-01-23",
					"dateRaw": "Friday"
				},
				"origin": {
					"city": "Dallas",
					"state": null,
					"rawText": "Dallas"
				},
				"driverType": null,
				"destinationPreference": {
					"type": "region",
					"region": "Midwest",
					"primaryCity": null,
					"primaryState": null,
					"acceptableDestinations": null,
					"rawText": "looking Midwest"
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.75,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields"
					]
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.75,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields",
				"hallucination_corrected"
			]
		},
		"inferences": {
			"fields": [
				"availabilityBatch.trucks.0.origin.state"
			],
			"severity": "medium"
		}
	}
}
```

</details>

---

## 7. Minimal / No Details

**Input:**
```json
{
  "messageId": "sample-007",
  "from": "unknown@carrier.com",
  "to": "loads@broker.com",
  "date": "2026-01-19T12:00:00Z",
  "subject": "Capacity",
  "text": "Have capacity."
}
```

<details>
<summary><b>Output Sample</b></summary>


```json
{
	"carrier": {
		"mcNumber": null,
		"companyName": null
	},
	"contact": null,
	"availabilityBatch": {
		"sourceType": "email",
		"rawEmailText": "Have capacity.",
		"trucks": [
			{
				"truckCount": 1,
				"equipment": {
					"category": "unknown",
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
				"driverType": null,
				"destinationPreference": {
					"type": "unspecified",
					"region": null,
					"primaryCity": null,
					"primaryState": null,
					"acceptableDestinations": null,
					"rawText": null
				},
				"notes": null,
				"metadata": {
					"confidenceScore": 0.2,
					"requiresHumanReview": true,
					"reviewReasons": [
						"incomplete_core_fields",
						"low_confidence_score"
					]
				}
			}
		]
	},
	"metadata": {
		"extraction": {
			"confidenceScore": 0.2,
			"requiresHumanReview": true,
			"reviewReasons": [
				"incomplete_core_fields",
				"low_confidence_score"
			]
		},
		"inferences": {
			"fields": []
		}
	}
}
```

</details>