# ParkSahayMQTTBroker

A self-hosted MQTT broker solution for the ParkSahay IoT system.

## Overview

This repository contains the configuration for a self-hosted Mosquitto MQTT broker using Docker, designed to be deployed on Render as a private service.

## Architecture

- **ESP32 Modules** → **MQTT Broker (Mosquitto)** → via topic: sensors/module-id/status
- **Node.js Subscriber** (on Render) that listens to messages from broker
- **Frontend** (Vercel) that hits /status endpoint from the subscriber to show real-time updates

## Files

- `Dockerfile`: Configures the Docker image based on eclipse-mosquitto:2.0
- `mosquitto.conf`: Configuration for the MQTT broker
- `render.yaml`: Configuration for deployment on Render

## Deployment

### Self-Host Mosquitto on Render

1. Create a new Private Web Service on Render
2. Deploy this repository
3. Render will assign a private internal hostname (e.g., mqtt-broker-name.internal)
4. Your Node.js server can use that hostname to connect

### Connection Details

ESP32 modules should connect to:
```
mqtt://<public IP or internal hostname>:1883
```

## Authentication

Currently, authentication is disabled (`allow_anonymous true`). To enable authentication:

1. Set `allow_anonymous false` in mosquitto.conf
2. Create a passwd file with user credentials
3. Update the Dockerfile to copy the passwd file
