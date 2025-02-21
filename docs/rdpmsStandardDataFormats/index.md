# RDPMS Standard Data Formats

## Overview
This page provides an overview of the various payload formats used within the **RDPMS system**. It follows **oneM2M standard data formats** to ensure **interoperability** between Station Gateways, IoT devices, sensors, and Application Software. These standards enable seamless communication between application software of different OEMs.

???+ question "Why oneM2M Standards?"
    The **oneM2M standard** ensures a unified framework for IoT/M2M communication, making sure different devices and software solutions from multiple vendors can work together without compatibility issues.

**Note**: Vendors should acquire a basic understanding of **oneM2M standards**. [Refer to oneM2M Guidelines](https://coi.cdot.in/docs/oneM2MGuideline.html).

## Data Flow & Containers in CCSP Layer

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

## Types of Containers in Standard Data Format

???+ example "Different Containers"
    - ### <u>**Station Gateway Connect Container**</u>: 
    Created by the station gateway on the CCSP Layer, subscribed by the cloud app. It notifies the application software when a station gateway connects, reboots, or recovers from a power failure.

    - ### <u>**Station Gateway Information Container**</u>: 
    Created by the station gateway on the CCSP Layer, subscribed by the cloud app. It sends installation details and updates when sensors/IoT devices are added or removed. This occurs at least once a month and should be configurable.

    - ### <u>**Registration Process**</u>: 
    An initial copy of information container data is uploaded by a railway admin via an Excel sheet. The application software cross-checks data received from the station gateway against the uploaded data and provides an error message if inconsistencies exist.

    - ### <u>**Image Container**</u>: 
    Created by the station gateway, subscribed by the cloud app. It provides a snapshot of all parameter values at a defined interval (default: 24 hours, configurable).

    - ### <u>**Parameter Container**</u>: 
    Created by the station gateway, subscribed by the cloud app. It sends data when: a parameter changes by ±2% in the last 5 seconds or specific parameters (e.g., voltage/current of certain equipment) are sampled every 20 ms over 5 seconds or a packet is sent every 5 seconds with these values.

    - ### <u>**Diagnostic Container**</u>: 
    Created by the station gateway, subscribed by the cloud app. It reports the health status of all sensors/IoT devices when a fault occurs or at a configurable interval (default: 12 hours).

    - ### <u>**Time Sync Container**</u>: 
    Created and subscribed by the station gateway. The application software writes to it, sending a time synchronization request to the station gateway at first connection or at a configurable interval (default: 24 hours).

    - ### <u>**Time Sync Acknowledgment Container**</u>: 
    Created by the station gateway, subscribed by the cloud app. It sends an acknowledgment after the time sync process is completed.

    - ### <u>**Configuration Container**</u>: 
    Created and subscribed by the station gateway. The application software writes configuration updates, which are then received by the station gateway.

    - ### <u>**Configuration Acknowledgment Container**</u>: 
    Created by the station gateway, subscribed by the cloud app. It sends an acknowledgment once a configuration update is processed.

    - ### <u>**Station Gateway Status Container**</u>: 
    Created by the CCSP Layer. The station gateway sends an initial content instance to inform CCSP that all containers have been created, allowing access control policies to be activated.

## Key Takeaways
- The **RDPMS system** uses **oneM2M-compliant data formats** to standardize railway IoT communication.
- **CCSP Layer** plays a crucial role in **device authentication**, **data integrity**, and **subscription-based data flow**.
- Data can flow **bidirectionally** between Station Gateways and Application Software.
- **CCSP is hosted in the Railway Cloud** for enhanced security and interoperability.
- The adoption of oneM2M standards enhances **data security, interoperability, and reliability** of RDPMS across multiple vendors and systems.
