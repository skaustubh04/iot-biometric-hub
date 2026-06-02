
# RPi Enabled IoT Server

A real-time biometric data acquisition and logging system built on an edge-gateway architecture.

## Architecture
- **Data Acquisition:** ESP8266 + MAX30102 sensor (captures HR and SpO2).
- **Middleware:** MQTT (Mosquitto) for asynchronous message queuing.
- **Processing/UI:** Node-RED for flow orchestration and dashboard visualization.
- **Storage:** SQLite3 relational database managed via a custom Bash CLI.

## Key Features
- **Automated Logging:** Data is ingested via MQTT and persisted into SQLite via Node-RED.
- **Bash CLI Utility:** A menu-driven interface (`bash_script.sh`) allowing users to query trends, calculate averages, and compare biometric readings across multiple users without writing raw SQL.
- **Real-time Monitoring:** Node-RED dashboard provides live graphical visualization of HR and SpO2 trends.

## Setup & Execution
- Ensure `mosquitto` and `node-red` are running.
- Make the script executable: `chmod +x bash_script.sh`
- Run the tool: `./bash_script.sh`
