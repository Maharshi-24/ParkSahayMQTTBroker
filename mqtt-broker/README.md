# Mosquitto MQTT Broker for ParkSahay

This directory contains the configuration for a self-hosted Mosquitto MQTT broker using Docker on Render.

## Files

- `Dockerfile`: Configures the Docker image based on eclipse-mosquitto:2.0
- `mosquitto.conf`: Basic configuration for the MQTT broker
  
## Deployment Instructions

1. Deploy this repository as a private service on Render
2. Render will assign a private internal hostname (e.g., mqtt-broker-name.internal)
3. Your Node.js server can use that hostname to connect

## Connection Details

ESP32 modules should connect to:
```
mqtt://<public IP or internal hostname>:1883
```

## Authentication

Currently, authentication is disabled (`allow_anonymous true`). To enable authentication:

1. Set `allow_anonymous false` in mosquitto.conf
2. Create a passwd file with user credentials
3. Update the Dockerfile to copy the passwd file
