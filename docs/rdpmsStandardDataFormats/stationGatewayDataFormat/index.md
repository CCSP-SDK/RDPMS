# Station Gateway Standard Data Format

## Introduction
The **Station Gateway Standard Data Format** defines the structure of communication between the **Station Gateway**, **CCSP (Common Communication Service Platform)**, and cloud applications. Each message follows the oneM2M standard and is transmitted over MQTT or HTTP. The requests and responses for various operations follow a standardized JSON payload structure.

This page provides a detailed breakdown of different message types, including their payloads and responses.

---

## Station Gateway AE Registration Request (One-Time)

**Request Details**
    ```yaml
    - Broker URL: `mqtts://ccsp.m2m.cdot.in`
    - Topic: `/oneM2M/reg_req/<STATION-GW-AE-ID>/<registrarCseId>/json`
    ```
### Request Payload
| Field  | Description  |
|--------|-------------|
| `op`   | Operation code (1 for create request) |
| `to`   | Destination resource ID |
| `fr`   | Sender (Station Gateway AE ID) |
| `rqi`  | Unique request identifier |
| `ty`   | Resource type (2 for AE registration) |
| `pc`   | Payload content |

```json
{
  "op": 1,
  "to": "<registrarCseBaseResourceId>",
  "fr": "<STATION-GW-AE-ID>",
  "rqi": "<unique-Request-Identifier>",
  "ty": 2,
  "pc": {
    "m2m:ae": {
      "api": "<app-ID>",
      "rr": "true",
      "srv": ["3"],
      "acpi": ["<ACP-Resource-Id>"],
      "poa": ["mqtts://ccsp.m2m.cdot.in/oneM2M/req/CSE001/<STATION-GW-AE-ID>/json"]
    }
  },
  "rvi": "3"
}
```

### Response Payload
| Field  | Description  |
|--------|-------------|
| `rsc`  | Response status code (2001 for successful creation) |
| `rqi`  | Unique request identifier |
| `pc`   | Response content |

```json
{
  "rsc": 2001,
  "rqi": "<unique-Request-Identifier>",
  "pc": {
    "m2m:ae": {
      "ty": 2,
      "ri": "SWGwg21074",
      "pi": "R0",
      "ct": "20240229T152015",
      "lt": "20240229T152015",
      "rn": "ae18860",
      "acpi": ["R23"],
      "et": "20290227T142647",
      "api": "Ra1.com.cdot.smartCity",
      "aei": "SWGwg21074",
      "rr": true,
      "srv": ["3"],
      "poa": ["mqtts://ccsp.m2m.cdot.in/oneM2M/req/CSE001/SWGwg21074/json"]
    }
  },
  "rvi": "3"
}
```

---

## Station Gateway Connect Container (With Time Sync Request)

### Request Payload
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
      "rn": "STN_GW_CONNECT_CNT",
      "acpi": ["<ACP-Resource-Id>"]
    }
  },
  "rvi": "3"
}
```

### Response Payload
```json
{
  "rsc": 2001,
  "rqi": "<unique-Request-Identifier>",
  "pc": {
    "m2m:cnt": {
      "ty": 3,
      "ri": "R51185",
      "pi": "SWGwg21074",
      "ct": "20240229T163926",
      "lt": "20240229T163926",
      "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
      "rn": "STN_GW_CONNECT_CNT",
      "acpi": ["R248241"],
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

