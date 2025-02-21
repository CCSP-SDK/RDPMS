# RDPMS Standard Data Formats

## Overview
This page provides an overview of the various payload formats used within the **RDPMS system**. It follows **oneM2M standard data formats** to ensure **interoperability** between Station Gateways, IoT devices, sensors, and Application Software. These standards enable seamless communication between application software of different OEMs.

???+ question "Why oneM2M Standards?"
    The **oneM2M standard** ensures a unified framework for IoT/M2M communication, making sure different devices and software solutions from multiple vendors can work together without compatibility issues.

**Note**: Vendors should acquire a basic understanding of **oneM2M standards**. [Refer to oneM2M Guidelines](https://coi.cdot.in/docs/oneM2MGuideline.html).

## Data Flow & Containers in CCSP Layer

### Registration Process: 
An initial copy of information container data is uploaded by a railway admin via an Excel sheet. The application software cross-checks data received from the station gateway against the uploaded data and provides an error message if inconsistencies exist.

### How Data is Organized
The **CCSP Layer** (C-DOT Common Service Platform) organizes data using **containers**. These containers act as storage units where **data instances** are managed.

???+ tip "Container Data Flow"
    - **Containers** are created by the **Station Gateway** in the CCSP Layer.
    - **Data Instances** are sent by the **Station Gateway** to these containers.
    - **Applications & Other Entities** subscribe to these containers to receive notifications when new data instances are added.

### Bidirectional Communication
- The **Application Software** can also create data instances in certain containers.
- The **Station Gateway** subscribes to these containers and receives data instances as notifications.

### Role of CCSP Layer

???+ info "Authentication & Data Integrity"
    - Ensures that **only authenticated devices** can send or receive data.
    - Verifies that data follows **oneM2M standard formats** before forwarding it to RDPMS Application Software.


## Key Takeaways
- The **RDPMS system** uses **oneM2M-compliant data formats** to standardize railway IoT communication.
- **CCSP Layer** plays a crucial role in **device authentication**, **data integrity**, and **subscription-based data flow**.
- Data can flow **bidirectionally** between Station Gateways and Application Software.
- **CCSP is hosted in the Railway Cloud** for enhanced security and interoperability.
- The adoption of oneM2M standards enhances **data security, interoperability, and reliability** of RDPMS across multiple vendors and systems.
