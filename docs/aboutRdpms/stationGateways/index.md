# Station Gateway Overview

## Introduction
The **Station Gateway** is an embedded electronic unit deployed at each station to facilitate data acquisition, processing, and communication with the **RDPMS Application Software** hosted on the **Railway Cloud** via the **CCSP Layer**.

## Key Functions
- Receives data from **sensors** and **diagnostic ports** of station equipment.
- Converts and transmits data using **oneM2M Standard Data Format** and **MQTT Protocol**.
- Ensures **interoperability** across different vendor systems through standardized communication.
- Provides **event logging** to store up to **5 million events** or a **minimum of 10 days** of data.
- Supports **secure data transmission** and **remote access capabilities**.

## Communication & Security
- Converts data into **oneM2M format** before transmitting it to the **CCSP Layer**.
- Supports various transmission media, including **OFC, Ethernet, wireless networks, and voice channels**.
- Includes **12 configurable serial ports** for communication with station equipment.
- Implements **data security measures** to prevent unauthorized access.
- Complies with **TEC IoT Security Guidelines** and undergoes periodic cybersecurity audits.


## Conclusion

???+ example "Quick Summary"
    This **Station Gateway** serves as the critical interface between station-level data sources and the **CCSP Layer**, ensuring efficient, standardized, and secure data communication within the **RDPMS ecosystem**.

