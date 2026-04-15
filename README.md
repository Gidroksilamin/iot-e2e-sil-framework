# Status Bar SIL Test Framework

### Overview
This repository contains a **Software-in-the-Loop (SIL)** testing environment for the **Status Bar** IoT device. It is designed to validate the integration between the device firmware logic, cloud backend (MQTT), and local network interfaces (HTTP API) without requiring physical hardware.

The framework focuses on **End-to-End (E2E)** scenarios, data consistency, and system resilience under network instability.

### System Architecture
The environment is orchestrated using `docker-compose` and consists of the following isolated nodes:

* **Device Emulator (`device_mock`):** A Python-based digital twin of the Status Bar. It emulates a State Machine, handles MQTT commands from the Cloud, and provides a Local HTTP API (simulating Matter/LAN connectivity). It logs internal transitions to `stdout` (simulating UART).
* **Cloud Backend (`cloud_mock`):** A mock service representing the Cloud infrastructure. It provides a REST API for the test runner to trigger remote commands.
* **MQTT Broker (`mosquitto`):** The transport layer for device-to-cloud communication.
* **Test Runner (`pytest`):** The "Inquisitor" node. It triggers scenarios, intercepts traffic, and verifies internal device states via logs and API responses.

### Key Testing Scenarios
1.  **E2E State Consistency:** Change device status via Cloud API -> Verify MQTT payload -> Validate local device state via HTTP API.

### Tech Stack
* **Language:** Python 3.11+ (Asyncio)
* **Protocols:** MQTT (Paho), HTTP (FastAPI)
* **Orchestration:** Docker, Docker Compose
* **Testing:** Pytest, Requests