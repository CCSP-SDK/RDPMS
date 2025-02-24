# Station Gateway Standard Data Format

## Introduction
The **Station Gateway Standard Data Format** defines the structure of communication between the **Station Gateway**, **CCSP (Common Communication Service Platform)**, and cloud applications. Each message follows the oneM2M standard and is transmitted over MQTT or HTTP. The requests and responses for various operations follow a standardized JSON payload structure.

This page provides a detailed breakdown of different message types, including their payloads and responses.

---

## AE Registration Request (One-Time)

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<STATION-GW-AE-ID>/<registrarCseId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<registrarCseBaseResourceId>",
        "fr" : " <STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 2,
        "pc" : {
            "m2m:ae" : {
                "api" : "<app-ID>",
                "rr" : "true",
                "srv" : [ "3" ],
                "acpi" : [ "<ACP-Resource-Id>" ],
                "poa" : [ "mqtts://ccsp.m2m.cdot.in/oneM2M/req/CSE001/<STATION-GW-AE-ID>/json" ]
            } 
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway AE Reg Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R0",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 2,
        "pc" : {
            "m2m:ae" : {
                "api" : "Ra1.com.cdot.smartCity",
                "rr" : "true",
                "srv" : [ "3" ],
                "acpi" : [ "R23" ],
                "poa" : [ "mqtts://ccsp.m2m.cdot.in/oneM2M/req/CSE001/SWGwg21074/json" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:ae" : {
                "ty" : 2,
                "ri" : "SWGwg21074",
                "pi" : "R0",
                "ct" : "20240229T152015",
                "lt" : "20240229T152015",
                "rn" : "ae18860",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "api" : "Ra1.com.cdot.smartCity",
                "aei" : "SWGwg21074",
                "rr" : true,
                "srv" : [ "3" ],
                "poa" : [ "mqtts://ccsp.m2m.cdot.in/oneM2M/req/CSE001/SWGwg21074/json" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (2 for `<AE>`). |
    | `pc`   | Primitive Content of the request. |
    | `rvi`  | OneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


## Connect Container (with Time Sync Request) Creation & Subscription

```
## Creation from station gateway to CCSP
``` 
=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_CONNECT_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Connect Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_CONNECT_CNT",
                "acpi" : [ "R248241" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R51185",
                "pi" : "SWGwg21074",
                "ct" : "20240229T163926",
                "lt" : "20240229T163926",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_CONNECT_CNT",
                "acpi" : [ "R248241" ],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (2 for `<AE>`). |
    | `pc`   | Primitive Content of the request. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


```
## Subscription by Cloud to CCSP (created by station gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<connect-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<connect-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_CONNECT_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Connect Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R51185",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_CONNECT_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["SWGwg21be4"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R53190",
                "pi" : "R51185",
                "ct" : "20240229T164537",
                "lt" : "20240229T164537",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_CONNECT_SUB",
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : [ "SWGwg21be4" ],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation code (1 for create request). |
    | `to`   | Destination resource ID. |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique request identifier. |
    | `ty`   | Resource type (23 for Subscription). |
    | `pc`   | Primitive content. |
    | `rvi`  | OneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |



## Information Container Creation & Subscription (One-Time)

```
## Creation from station gateway to CCSP
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_INFO_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Information Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_INFO_CNT",
                "acpi" : [ "R248241" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R53191",
                "pi" : "SWGwg21074",
                "ct" : "20240229T164922",
                "lt" : "20240229T164922",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_INFO_CNT",
                "acpi" : [ "R248241" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


```
## Subscription by Cloud to CCSP (created by station gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<info-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<info-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_INFO_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "<cloud-AE-ID>", "<railway-cloud-endpoint>" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Information Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R53191",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_INFO_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "SWGwg21be4", "http://dummylocalhost" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R172402",
                "pi" : "R53191",
                "ct" : "20240301T113520",
                "lt" : "20240301T113520",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_INFO_SUB",
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : [ "SWGwg21be4", "http://dummylocalhost" ],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation code (1 for create request). |
    | `to`   | Destination resource ID. |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique request identifier. |
    | `ty`   | Resource type (23 for Subscription). |
    | `pc`   | Primitive content. |
    | `rvi`  | OneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |



## Parameter Container Creation & Subscription (One-Time)

```
## Creation from station gateway to CCSP
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_PARAMETER_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Parameter Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_PARAMETER_CNT",
                "acpi" : [ "R23" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R177532",
                "pi" : "SWGwg21074",
                "ct" : "20240301T113925",
                "lt" : "20240301T113925",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_PARAMETER_CNT",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Cloud to CCSP (created by station gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<parameter-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<parameter-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_PARAMETER_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "<cloud-AE-ID>", "<railway-cloud-endpoint>" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Parameter Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R177532",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_PARAMETER_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "SWGwg21be4", "http://dummyrailwayendpoint.com" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R185873",
                "pi" : "R177532",
                "ct" : "20240301T114646",
                "lt" : "20240301T114646",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_PARAMETER_SUB",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : [ "SWGwg21be4", "http://dummyrailwayendpoint.com" ],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```
=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


## Image Container Creation & Subscription (One-Time)

```
## Creation from station gateway to CCSP
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_IMAGE_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Image Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_IMAGE_CNT",
                "acpi" : [ "R23" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R189330",
                "pi" : "SWGwg21074",
                "ct" : "20240301T115008",
                "nu": [ "<cloud-AE-ID>", "<railway-cloud-endpoint>" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Cloud to CCSP (created by station gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<image-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<image-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_IMAGE_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "<cloud-AE-ID>", "<railway-cloud-endpoint>" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Image Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R189330",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_IMAGE_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "SWGwg21be4", "http://dummyrailwayendpoint.in" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R194055",
                "pi" : "R189330",
                "ct" : "20240301T115404",
                "lt" : "20240301T115404",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_IMAGE_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : [ "SWGwg21be4", "http://dummyrailwayendpoint.in" ],
                "nct" : 1
            }
        },
        "rvi": "3"
    }
    ```
=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


## Diagnostic Container Creation & Subscription (One-Time)

```
## Creation from Station Gateway to CCSP
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_DIAG_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Diagnostic Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_DIAG_CNT",
                "acpi" : [ "R23" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R196117",
                "pi" : "SWGwg21074",
                "ct" : "20240301T115643",
                "lt" : "20240301T115643",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_DIAG_CNT",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Cloud to CCSP (Created by Station Gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<diag-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<diag-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>" ],
                "rn": "STN_GW_DIAG_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "<Cloud-AE-ID>" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Diagnostic Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R196117",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn": "STN_GW_DIAG_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": [ "SWGwg21be4" ],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R199593",
                "pi" : "R196117",
                "ct" : "20240301T115954",
                "lt" : "20240301T115954",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_DIAG_SUB",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : [ "SWGwg21be4" ],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


## Time Sync Container Creation & Subscription (One-Time)

```
## Creation from Station Gateway to CCSP
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["<aplbl>_timesync", "<aplbl>", "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_TIMESYNC_CNT",
                "acpi" : ["<ACP-Resource-Id>"]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Time Sync Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["RDSOappLabel_timesync", "RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_TIMESYNC_CNT",
                "acpi" : ["R23"]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R206979",
                "pi" : "SWGwg21074",
                "ct" : "20240301T120640",
                "lt" : "20240301T120640",
                "lbl" : ["RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn" : "STN_GW_TIMESYNC_CNT",
                "acpi" : ["R23"],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Station Gateway to CCSP (Created by Station Gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<timesync-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<timesync-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["<aplbl>", "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_TIMESYNC_SUB",
                "acpi" : ["<ACP-Resource-Id>"],
                "enc" : { "net" : [3] },
                "nu": ["<STATION-GW-AE-ID>"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Time Sync Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R206979",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_TIMESYNC_SUB",
                "acpi" : ["R23"],
                "enc" : { "net" : [3] },
                "nu": ["SWGwg21074"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R210203",
                "pi" : "R206979",
                "ct" : "20240301T120906",
                "lt" : "20240301T120906",
                "lbl" : ["RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn" : "STN_GW_TIMESYNC_SUB",
                "acpi" : ["R23"],
                "enc" : { "net" : [3] },
                "nu" : ["SWGwg21074"],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |


## Configuration Container Creation & Subscription (One-Time)

```
## Creation from Station Gateway to CCSP (to be written by Cloud)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["<aplbl>_conf", "<aplbl>", "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_CONFIG_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Configuration Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["RDSOappLabel_conf", "RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_CONFIG_CNT",
                "acpi" : [ "R23" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R210723",
                "pi" : "SWGwg21074",
                "ct" : "20240301T121606",
                "lt" : "20240301T121606",
                "lbl" : ["RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn" : "STN_GW_CONFIG_CNT",
                "acpi" : ["R23"],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```
=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Station Gateway to CCSP (Created by Station Gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<conf-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<conf-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["<aplbl>", "<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_CONFIG_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["<STATION-GW-AE-ID>"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Configuration Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R210723",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_CONFIG_SUB",
                "acpi" : ["R23"],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["SWGwg21074"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R210734",
                "pi" : "R210723",
                "ct" : "20240301T121918",
                "lt" : "20240301T121918",
                "lbl" : ["RDSOappLabel", "12Z", "12ZDelhi", "12ZDelhi42"],
                "rn" : "STN_GW_CONFIG_SUB",
                "acpi" : ["R23"],
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : ["SWGwg21074"],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```
=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |



## Time Sync Acknowledgement Container Creation & Subscription (One-Time)

```
## Creation from Station Gateway to CCSP (to be written by Cloud)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_TIMESYNC_ACK_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Time Sync Acknowledgement Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_TIMESYNC_ACK_CNT",
                "acpi" : [ "R23" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R211238",
                "pi" : "SWGwg21074",
                "ct" : "20240301T122314",
                "lt" : "20240301T122314",
                "lbl" : ["12Z", "12ZDelhi", "12ZDelhi42"],
                "rn" : "STN_GW_TIMESYNC_ACK_CNT",
                "acpi" : ["R23"],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Cloud to CCSP (Created by Station Gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<time-sync-ack-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<time-sync-ack-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_TIMESYNC_ACK_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["<Cloud-AE-ID>"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Time Sync Acknowledgement Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R211238",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_TIMESYNC_ACK_CNT",
                "acpi" : ["R23"],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["SWGwg21be4"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R212084",
                "pi" : "R211238",
                "ct" : "20240301T122636",
                "lt" : "20240301T122636",
                "lbl" : ["12Z", "12ZDelhi", "12ZDelhi42"],
                "rn" : "STN_GW_TIMESYNC_ACK_CNT",
                "acpi" : ["R23"],
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : ["SWGwg21be4"],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |



## Configuration Acknowledgement Container Creation & Subscription (One-Time)

```
## Creation from Station Gateway to CCSP (Created by Station Gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/req/<STATION-GW-AE-ID>/CSE001/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<STATION-GW-AE-ID>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_CONFIG_ACK_CNT",
                "acpi" : [ "<ACP-Resource-Id>" ]
            }
        },
        "rvi" : "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Configuration Acknowledgement Container Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "SWGwg21074",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 3,
        "pc" : {
            "m2m:cnt" : {
                "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_CONFIG_ACK_CNT",
                "acpi" : [ "R23" ]
            }
        },
        "rvi" : "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:cnt" : {
                "ty" : 3,
                "ri" : "R222909",
                "pi" : "SWGwg21074",
                "ct" : "20240301T134607",
                "lt" : "20240301T134607",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_CONFIG_ACK_CNT",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "st" : 0,
                "cr" : "SWGwg21074",
                "mni" : 20,
                "mbs" : 1048576,
                "mia" : 864000,
                "cni" : 0,
                "cbs" : 0
            }
        },
        "rvi" : "3"
    }
    ```

=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

```
## Subscription by Cloud to CCSP (Created by Station Gateway)
```

=== "Request Sample"

    ```yaml
    Request Details:
    Broker URL: mqtts://ccsp.m2m.cdot.in
    Topic: /oneM2M/reg_req/<configuration-ack-container-ResourceId>/json
    ```

    ```json
    {
        "op" : 1,
        "to" : "<configuration-ack-container-ResourceId>",
        "fr" : "<STATION-GW-AE-ID>",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["<zone_code>", "<zone_code><division_code>", "<zone_code><division_code><sc>"],
                "rn": "STN_GW_CONFIG_ACK_SUB",
                "acpi" : [ "<ACP-Resource-Id>" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["<Cloud-AE-ID>"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

=== "Request & Response Sample With Data"

    ```yaml
    Station Gateway Configuration Acknowledgement Subscription Request
    ```

    ```json
    {
        "op" : 1,
        "to" : "R222909",
        "fr" : "SWGwg21074",
        "rqi" : "<unique-Request-Identifier>",
        "ty" : 23,
        "pc" : {
            "m2m:sub" : {
                "lbl": ["12Z", "12ZDelhi", "12ZDelhi42"],
                "rn": "STN_GW_CONFIG_ACK_SUB",
                "acpi" : [ "R23" ],
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu": ["SWGwg21be4"],
                "nct": 1
            }
        },
        "rvi": "3"
    }
    ```

    ```yaml
    Response
    ```

    ```json
    {
        "rsc" : 2001,
        "rqi" : "<unique-Request-Identifier>",
        "pc" : {
            "m2m:sub" : {
                "ty" : 23,
                "ri" : "R222910",
                "pi" : "R222909",
                "ct" : "20240301T134817",
                "lt" : "20240301T134817",
                "lbl" : [ "12Z", "12ZDelhi", "12ZDelhi42" ],
                "rn" : "STN_GW_CONFIG_ACK_SUB",
                "acpi" : [ "R23" ],
                "et" : "20290227T142647",
                "cr" : "SWGwg21074",
                "enc" : {
                    "net" : [ 3 ]
                },
                "nu" : [ "SWGwg21be4" ],
                "nct" : 1
            }
        },
        "rvi" : "3"
    }
    ```
    
=== "Field Descriptions"
    | Field  | Description  |
    |--------|-------------|
    | `op`   | Operation Code (1 for create request). |
    | `to`   | Destination Resource ID (Target CSE resource ID). |
    | `fr`   | Sender (Station Gateway AE ID). |
    | `rqi`  | Unique Request Identifier to track the request. |
    | `ty`   | Resource Type (3 for Container). |
    | `pc`   | Primitive content. |
    | `rvi`  | oneM2M Release Version Indicator. |
    | `rsc`  | Response status code (2001: Created). |

