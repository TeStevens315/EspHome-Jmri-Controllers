# ESPHome Turnout Control (tc-1.yaml)

## Overview

This configuration controls up to 8 model railroad turnouts using an ESP32 and relay or H-bridge drivers. Each turnout is controlled by two GPIO outputs (A and B) and triggered by MQTT messages. The system is designed for integration with JMRI or other automation systems via MQTT.

## How it Works

- Each turnout is controlled by sending an MQTT message to a topic like `track/turnout/TO-1-N` (N = turnout number).
- The payload should be `THROWN` or `CLOSED`.
- The ESP32 pulses the appropriate output for a configurable time (`turnout_pulse_ms`), then turns both outputs off to avoid overheating the coil.
- All pin assignments are listed in the `output:` section.

## Hardware Setup

- ESP32 (32-pin recommended)
- Each turnout requires two GPIO outputs (A and B)
- Connect outputs to relay or H-bridge driver circuits for each turnout coil
- See the YAML comments for pin mapping

## Usage

1. Flash the ESP32 with this config using ESPHome.
2. Connect to your WiFi and MQTT broker (set credentials in `secrets.yaml`).
3. Send MQTT messages to control turnouts:
   - Topic: `track/turnout/TO-1-1` (for turnout 1), etc.
   - Payload: `THROWN` or `CLOSED`
4. The ESP32 will pulse the turnout coil for the set time, then turn off.

## Customization

- Change `esp_id` in `substitutions:` to set the controller number.
- Adjust `turnout_pulse_ms` for your turnout hardware.
- Add or remove turnouts by editing the `mqtt.on_message` and `output` sections.

## Troubleshooting

- Ensure your MQTT broker and credentials are correct.
- Check wiring and pin assignments for each turnout.
- Use the ESPHome logs for debugging (set `logger.level: DEBUG`).
