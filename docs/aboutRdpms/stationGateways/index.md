# About Station Gateways

## Station Gateway Overview
At each station, there shall be one embedded electronic unit called **Station Gateway**. It shall:

- Receive raw data/parameter values from **Sensors** through IoT devices.
- Collect data from **diagnostic ports** of various equipment for **Signalling assets**.
- Transmit data to the **RDPMS Application software** hosted at the **Railway cloud** via the **CCSP Layer** (C-DOT Common Service Platform).
- Use **Standard oneM2M Data format** and **MQTT Protocol** for communication.
- Function as an **Edge Computing Device** at the station.

## Features of Station Gateway
- **Inbuilt Protocol Converters**: Ensuring connectivity with:
  - Datalogger
  - IPS (Integrated Power Supply)
  - Other equipment as referenced in clauses **3.3 & 4** of this document.
- **Diagnostic Features**: Allows monitoring and troubleshooting.
- **Configuration Capabilities**: Details are provided in **Annexure A & B**.


