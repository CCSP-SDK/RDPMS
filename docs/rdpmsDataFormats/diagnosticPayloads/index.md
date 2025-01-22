# Diagnostic Payloads

## Creation from Station Gateway to CCSP

### Request to Create Diagnostic Container

```json
{
  "op": 1,
  "to": "<STATION-GW-AE-ID>",
  "fr": "<STATION-GW-AE-ID>",
  "rqi": "<unique-Request-Identifier>",
  "ty": 3,
  "pc": {
    "m2m:cnt": {
      "lbl": ["<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
      "rn": "STN_GW_DIAG_CNT",
      "acpi": ["<ACP-Resource-Id>"]
    }
  },
  "rvi": "3"
}
```

### Request to Create Diagnostic Subscription

```json
{
  "op": 1,
  "to": "<diag-container-ResourceId>",
  "fr": "<STATION-GW-AE-ID>",
  "rqi": "<unique-Request-Identifier>",
  "ty": 23,
  "pc": {
    "m2m:sub": {
      "lbl": ["<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
      "rn": "STN_GW_DIAG_SUB",
      "acpi": ["<ACP-Resource-Id>"],
      "enc": {
        "net": [3]
      },
      "nu": ["<Cloud-AE-ID>"],
      "nct": 1
    }
  },
  "rvi": "3"
}
```

### Sample Request/Response for Diagnostic Container

```
Request
```

```json
{
  "op": 1,
  "to": "SWGwg21074",
  "fr": "SWGwg21074",
  "rqi": "<unique-Request-Identifier>",
  "ty": 3,
  "pc": {
    "m2m:cnt": {
      "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
      "rn": "STN_GW_DIAG_CNT",
      "acpi": ["R23"]
    }
  },
  "rvi": "3"
}
```
```
Response
```

```json
{
  "rsc": 2001,
  "rqi": "<unique-Request-Identifier>",
  "pc": {
    "m2m:cnt": {
      "ty": 3,
      "ri": "R196117",
      "pi": "SWGwg21074",
      "ct": "20240301T115643",
      "lt": "20240301T115643",
      "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
      "rn": "STN_GW_DIAG_CNT",
      "acpi": ["R23"],
      "et": "20290227T142647",
      "st": 0,
      "cr": "SWGwg21074",
      "mni": 20,
      "mbs": 1048576,
      "mia": 864000,
      "cni": 0,
      "cbs": 0
    }
  },
  "rvi": "3"
}
```

### Sample Request/Response for Diagnostic Subscription

```
Request
```
```json
{
  "op": 1,
  "to": "R196117",
  "fr": "SWGwg21074",
  "rqi": "<unique-Request-Identifier>",
  "ty": 23,
  "pc": {
    "m2m:sub": {
      "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
      "rn": "STN_GW_DIAG_SUB",
      "acpi": ["R23"],
      "enc": {
        "net": [3]
      },
      "nu": ["SWGwg21be4"],
      "nct": 1
    }
  },
  "rvi": "3"
}
```
```
Response
```

```json
{
  "rsc": 2001,
  "rqi": "<unique-Request-Identifier>",
  "pc": {
    "m2m:sub": {
      "ty": 23,
      "ri": "R199593",
      "pi": "R196117",
      "ct": "20240301T115954",
      "lt": "20240301T115954",
      "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
      "rn": "STN_GW_DIAG_SUB",
      "acpi": ["R23"],
      "et": "20290227T142647",
      "cr": "SWGwg21074",
      "enc": {
        "net": [3]
      },
      "nu": ["SWGwg21be4"],
      "nct": 1
    }
  },
  "rvi": "3"
}
```

