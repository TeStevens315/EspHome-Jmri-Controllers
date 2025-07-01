# ESPHome JMRI Controllers

This is a collection of ESPHome controllers designed to integrate with JMRI (Java Model Railroad Interface) wirelessly. These controllers enable seamless communication between your model railroad layout and JMRI software using wireless protocols.

## Overview

The controllers in this repository provide wireless connectivity for various model railroad components, allowing you to control and monitor your layout remotely through JMRI without the need for physical wired connections.

## Requirements

### Essential Requirements

- **MQTT Broker**: A working MQTT broker is required for communication between the ESPHome devices and JMRI
- **ESPHome**: ESPHome installation for compiling and uploading firmware to ESP devices

### Optional Requirements

- **Home Assistant**: Required for some controllers that integrate with Home Assistant for additional automation and monitoring capabilities

## Controllers Included

- **TC-1 Controller** (`tc-1.yaml`) - Turnout control controller
- **TC-Servo Controller** (`tc-servo.yaml`) - Servo-based turnout controller

## Getting Started

1. Set up your MQTT broker
2. Configure your WiFi and MQTT credentials in `secrets.yaml`
3. Compile and upload the desired controller firmware using ESPHome
4. Configure JMRI to communicate with the controllers via MQTT

## Documentation

Each controller has its own detailed documentation:

- [TC-1 Controller README](README-tc-1.md)
- [TC-Servo Controller README](README-tc-servo.md)

## Configuration

Make sure to update the `secrets.yaml` file with your specific network and MQTT broker settings before compiling any of the controller firmware.

## Contributing

Feel free to contribute additional controllers or improvements to existing ones. Please ensure all new controllers follow the established patterns for MQTT communication and JMRI integration.
