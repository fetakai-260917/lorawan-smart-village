# Design and Deployment of a LoRaWAN-Based Smart Village IoT System

**SEEDs LLP – D-Lab**

---

## Links

- 🔗 Project Website (Smart Village): [https://seeds-dlab.com/en/smart-village](https://seeds-dlab.com/en/smart-village)

- 🚀 Live Dashboard Demo (Node-RED): [https://farmer-a.seeds-dlab.com/dashboard](https://farmer-b.seeds-dlab.com/dashboard)

  Real-time monitoring and alert interface for field-deployed sensor and system data.

---

## Overview

This project presents the design, implementation, and real-world deployment of an end-to-end **LoRaWAN-based IoT system for smart village and rural monitoring applications**.

The system integrates edge devices, wireless communication, gateway infrastructure, backend services, data storage, visualization, edge AI, and digital-twin technologies.

The platform supports practical use cases including:

- Environmental monitoring
- Smart agriculture
- GPS-based asset tracking
- Edge AI wildlife detection
- Real-time alerts
- Digital-twin visualization
- Experimental resilient gateway communication
- Field deployment primarily in Japan

The project has evolved from a conventional LoRaWAN monitoring platform into a broader **edge-to-cloud field infrastructure** combining sensing, communications, local computation, backend processing, and operational visualization.

The primary deployment and field-validation environment is in **Japan**, with additional development and comparative testing carried out in **Germany**.

---

## System Architecture

Edge Devices → LoRaWAN Gateway → ChirpStack → MQTT → Node-RED → InfluxDB → Visualization

![System Architecture](docs/LoRaWAN-architecture-v2.png)

The main IoT data flow is:

```text
Edge Devices
    ↓
LoRaWAN
    ↓
LoRaWAN Gateway
    ↓
ChirpStack
    ↓
MQTT
    ↓
Node-RED
    ↓
InfluxDB
    ↓
Grafana / Node-RED Dashboard
```

---

## System Description

The system is designed as an end-to-end IoT infrastructure based primarily on LoRaWAN.

Edge devices collect environmental, agricultural, and positional data and transmit measurements through LoRaWAN.

Field devices include:

- Custom Arduino-based sensor nodes
- Environmental sensors
- GPS trackers
- Soil and water monitoring devices
- Raspberry Pi-based edge systems
- Commercial LoRaWAN devices

Multiple self-deployed LoRaWAN gateways receive uplink messages and forward them to a ChirpStack network server.

ChirpStack manages device registration, LoRaWAN communication, gateways, uplinks, downlinks, and network-level device management.

Application data is forwarded through MQTT to backend services, where Node-RED performs:

- Payload decoding
- Data transformation
- Filtering
- Routing
- Automation
- Alert handling
- Dashboard updates

Time-series sensor measurements are stored in InfluxDB and visualized through Grafana and custom Node-RED dashboards.

Backend components are primarily deployed using Docker on Linux-based infrastructure.

---

## Digital Twin & Field Monitoring

The project also includes a web-based **Digital Twin** providing a unified operational view of deployed IoT infrastructure.

Instead of viewing sensor, gateway, GPS, and AI information through separate systems, the Digital Twin integrates multiple data sources into a common interface.

### Integrated Information

- Environmental sensor measurements
- GPS tracker positions
- LoRaWAN gateway locations
- TSUNAGU relay locations
- Gateway and relay topology
- Field infrastructure status
- Edge AI wildlife detection events
- Event video playback
- Operational monitoring information

### Digital Twin Data Flow

```text
Physical Environment
        ↓
Sensors / GPS / Cameras
        ↓
LoRaWAN / Edge Processing
        ↓
ChirpStack / MQTT / REST APIs
        ↓
Backend Services
        ↓
Digital Twin
        ↓
Map / Monitoring / Event Visualization
```

The Digital Twin is deployed as a containerized web application and communicates with backend APIs providing sensor, gateway, location, and event information.

Its purpose is to provide a practical operational interface for understanding the state of distributed field infrastructure.

---

## Edge AI / Computer Vision System

In addition to the LoRaWAN infrastructure, the system incorporates an edge-based computer vision module for wildlife detection and monitoring.

![Computer Vision Architecture](docs/Edge-AI-architecture-v2.png)

### Description

A lightweight computer vision system is deployed on a Raspberry Pi to detect wildlife activity locally.

The basic processing flow is:

```text
Camera / Video Input
        ↓
Raspberry Pi Edge Device
        ↓
Local AI Inference
        ↓
Wildlife Event Detection
        ↓
Alert / Event Generation
        ↓
Backend API
        ↓
Digital Twin / Monitoring Interface
```

Key characteristics include:

- Detection is performed locally on the edge device
- Only relevant events need to be uploaded
- Events can trigger alerts to users
- Detection results can be displayed in the Digital Twin
- Event videos can be associated with detected activity
- Continuous cloud-based video processing is not required

This reduces cloud dependency and makes the system more suitable for rural environments where connectivity or bandwidth may be limited.

---

## Resilient Communications — TSUNAGU

The project also includes ongoing development of **TSUNAGU**, an experimental resilient communication architecture designed for field environments where conventional IP connectivity may be unavailable or disrupted.

Standard LoRaWAN deployments normally assume that gateways have IP connectivity to a network server.

TSUNAGU explores an additional gateway-to-gateway LoRa relay layer that allows traffic from remote field locations to be forwarded toward a border gateway with backend connectivity.

### Public-Facing System Overview

The following diagram shows the broader system at a deliberately high level.

![TSUNAGU Public System Overview](docs/TSUNAGU-public-overview.png)

It illustrates how field sensors, relay gateways, backend services, and Digital Twin applications fit together while intentionally omitting product-specific implementation details from the public-facing architecture.

### High-Level Concept

```text
LoRaWAN Sensor
      ↓
Relay Gateway
      ↓
Relay Gateway
      ↓
Border Gateway
      ↓
Backend Services
      ↓
Digital Twin / Applications
```

The concept is intended to support communication from remote or temporarily disconnected field locations without requiring every gateway to maintain its own direct Internet connection.

### Development Areas

Current TSUNAGU work includes:

- Border and relay gateway architecture
- Raspberry Pi-based gateway systems
- Gateway-to-gateway LoRa communication
- Multi-hop relay experiments
- ChirpStack-compatible backend integration
- MQTT routing and monitoring
- Gateway topology visualization
- Digital Twin integration
- Degraded-network operation
- Off-grid power evaluation
- Solar and battery-powered relay testing
- Field testing in Japan

> **Project Status**
>
> TSUNAGU is currently under active development.
>
> This portfolio presents only selected architectural concepts and development results. Source code, operational configurations, security-related information, detailed routing logic, and implementation parameters are intentionally not published.

---

## Smart Agriculture & Environmental Monitoring

The platform supports custom environmental and agricultural monitoring devices.

Measurements can include:

- Air temperature
- Humidity
- Soil moisture
- Water temperature
- Water level
- Light intensity
- Atmospheric pressure
- Battery voltage

Sensor data is transmitted through LoRaWAN and processed using the same backend infrastructure.

Selected devices also support remote control using LoRaWAN downlinks.

This enables monitoring and control applications such as irrigation and pump operation alongside sensor data acquisition.

---

## GPS Tracking

The system includes GPS-based tracking for assets and mobility applications.

GPS devices transmit location information using LoRaWAN.

Position data can be visualized through:

- Node-RED dashboards
- Web-based maps
- Digital Twin interfaces
- Lightweight Google Apps Script-based tracking interfaces

This allows the same LoRaWAN infrastructure to support both stationary sensors and mobile assets.

---

## Monitoring & Alerts

Node-RED is used as the primary integration and automation layer.

It performs functions including:

- MQTT message handling
- LoRaWAN payload decoding
- Data transformation
- Device filtering
- Event deduplication
- Alert generation
- Dashboard updates
- Database integration
- API communication
- Device downlink control

The system supports notifications through services such as:

- LINE
- Slack
- Email

This enables field events and system conditions to trigger near-real-time notifications.

---

## Features

- Real-time environmental monitoring
- Smart agriculture monitoring
- GPS-based asset tracking
- Custom LoRaWAN edge devices
- Multiple self-deployed LoRaWAN gateways
- Edge-based wildlife detection
- Event-triggered alerting
- Digital Twin visualization
- Gateway and relay topology visualization
- End-to-end MQTT-based data pipeline
- Time-series data storage
- Grafana visualization
- Node-RED operational dashboards
- Docker-based backend deployment
- Raspberry Pi edge computing
- Experimental resilient gateway communication
- Primary real-world field deployment in Japan

---

## Deployment Context

This system is based on real-world deployment rather than a laboratory-only implementation.

The **main field deployment is in Japan**, where the Smart Village infrastructure has been developed and tested under real operating conditions.

Deployment activities include:

- Multiple self-deployed LoRaWAN gateways
- Outdoor LoRaWAN coverage testing
- Field-deployed environmental sensors
- GPS tracker deployment
- Smart agriculture monitoring
- Raspberry Pi-based edge systems
- Wildlife monitoring
- TSUNAGU gateway relay experiments
- Solar and battery-powered gateway testing

### Japan — Primary Deployment

Japan is the project's primary deployment environment and the main location for:

- Smart Village field infrastructure
- LoRaWAN gateway deployment
- Environmental sensor operation
- Smart agriculture applications
- GPS-based tracking
- Wildlife monitoring
- TSUNAGU relay testing
- Digital Twin integration

### Germany — Additional Development & Testing

Additional development and comparative testing have been carried out in Germany.

These activities have included:

- LoRaWAN gateway testing
- EU868 operation
- Gateway relay experiments
- Power-consumption testing
- Off-grid gateway evaluation
- Backend and Digital Twin development

This provides useful comparative experience across different LoRaWAN frequency plans, infrastructure conditions, and deployment environments while keeping **Japan as the primary real-world deployment context**.

---

## My Role

My work covers the system from edge devices and wireless communication through backend infrastructure and visualization.

### LoRaWAN & Network Infrastructure

- Designed and deployed LoRaWAN network architecture
- Installed and configured multiple LoRaWAN gateways
- Configured and managed ChirpStack infrastructure
- Managed LoRaWAN device and gateway communication
- Conducted field coverage and connectivity testing
- Developed experimental gateway-relay architecture

### Edge Devices

- Custom-built Arduino-based sensor devices
- Integrated environmental sensors
- Implemented GPS tracking devices
- Configured LoRaWAN communication
- Developed sensor payload formats
- Implemented LoRaWAN uplink and downlink communication

### Backend Infrastructure

- Built MQTT-based data pipelines
- Developed Node-RED processing workflows
- Integrated InfluxDB time-series storage
- Built Grafana and Node-RED dashboards
- Deployed backend services using Docker
- Managed Linux-based server infrastructure

### Edge AI

- Integrated Raspberry Pi-based computer vision
- Implemented wildlife event detection
- Developed event-triggered alert workflows
- Integrated AI event data and video with backend services

### Digital Twin

- Integrated sensor, GPS, gateway, and AI event information
- Integrated REST API-based backend services
- Implemented gateway and relay visualization
- Integrated wildlife detection events
- Integrated video playback
- Managed containerized frontend deployment

### Resilient Communications

- Developed the TSUNAGU gateway-relay concept
- Configured border and relay gateway roles
- Conducted multi-hop LoRa relay experiments
- Integrated gateway relay information with backend monitoring
- Evaluated off-grid relay power requirements
- Integrated gateway topology with the Digital Twin

### Web & Infrastructure

- Developed and deployed the company website using HTML/CSS and Python/Flask
- Managed public web services and APIs
- Implemented secure service exposure using Cloudflare Tunnel
- Avoided direct public port forwarding for selected services

### GPS Visualization

- Built a lightweight GPS tracking interface using Google Apps Script
- Enabled real-time visualization of LoRaWAN-based positional data

---

## Results

- Successfully deployed multiple LoRaWAN gateways
- Achieved real-time environmental monitoring
- Achieved GPS-based asset tracking
- Built operational smart agriculture monitoring systems
- Built MQTT-based backend processing pipelines
- Implemented time-series storage using InfluxDB
- Built operational Grafana and Node-RED dashboards
- Implemented real-time alert workflows
- Integrated Raspberry Pi-based edge AI
- Integrated wildlife events into a Digital Twin interface
- Demonstrated system functionality through real-world deployment in Japan
- Conducted gateway-to-gateway LoRa relay experiments
- Evaluated off-grid and battery-powered gateway operation
- Integrated sensing, communications, data processing, AI, and visualization into a common infrastructure

---

## Tech Stack

### Wireless & IoT

- LoRa
- LoRaWAN
- ChirpStack
- MQTT
- Mosquitto

### Edge & Hardware

- Raspberry Pi
- Raspberry Pi Zero
- Arduino-compatible microcontrollers
- Seeed Studio XIAO
- LoRa-E5
- SX1302 / WM1302 LoRa concentrators
- GPS modules
- Environmental sensors

### Backend

- Linux
- Docker
- Node-RED
- Python
- Flask
- REST APIs

### Data

- InfluxDB
- PostgreSQL
- Redis

### Visualization

- Grafana
- Node-RED Dashboard
- Web-based maps
- Digital Twin

### Infrastructure

- Cloudflare
- Cloudflare Tunnel
- VPS / Linux servers
- Raspberry Pi gateway infrastructure

### Edge AI

- Computer vision
- Raspberry Pi-based inference
- Event-triggered video processing

---

## Current Development

Current development areas include:

- Resilient LoRa gateway communication
- TSUNAGU multi-hop gateway architecture
- Digital Twin integration
- Gateway topology visualization
- Edge AI event integration
- Off-grid gateway operation
- Solar-powered relay gateways
- Field resilience testing
- Integration of additional sensor systems

---

## Notes

This repository is based on real-world deployment and ongoing engineering work.

The public repository focuses on:

- System architecture
- Deployment methodology
- Technology integration
- Selected implementation examples
- Engineering results

Sensitive or operationally relevant information has intentionally been removed or anonymized.

This includes:

- Credentials
- API secrets
- Security keys
- Production configuration
- Internal network information
- Detailed TSUNAGU implementation
- Detailed routing and relay logic
- Proprietary scripts and workflows
- Sensitive infrastructure information

---

## About

This project is part of ongoing work at **SEEDs LLP – D-Lab** focused on practical IoT, edge computing, resilient communications, and digital infrastructure for field environments.

The project is primarily deployed and validated in **Japan**, with additional development and comparative testing performed in Germany.

The broader system concept can be summarized as:

```text
Physical Environment
        ↓
Sensing
        ↓
Edge Computing
        ↓
Wireless / Resilient Communication
        ↓
Data Infrastructure
        ↓
Digital Twin
        ↓
Operational Monitoring
```
