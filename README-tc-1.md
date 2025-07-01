# ESPHome Turnout Control (tc-1.yaml)

## Overview

This configuration controls up to 8 model railroad turnouts using an ESP32 and relay or H-bridge drivers. Each turnout is controlled by two GPIO outputs (A and B) and triggered by MQTT messages. The system is designed for integration with JMRI or other automation systems via MQTT.

## How it Works

- Each turnout is controlled by sending an MQTT message to a topic like `track/turnout/TO-1-N` (N = turnout number)
- The payload should be `THROWN` or `CLOSED`
- The ESP32 pulses the appropriate output for a configurable time (`turnout_pulse_ms`), then turns both outputs off to avoid overheating the coil
- All pin assignments are listed in the `output:` section

## Hardware Setup

### Required Components

- **ESP32** (32-pin recommended)
- **4x L298N H-Bridge modules** for 8 turnouts
- **Dupont connector cables** for easy wiring
- **ESP32 expansion board** (recommended)

### Hardware Connections

- Each turnout requires two GPIO outputs (A and B)
- Connect outputs to relay or H-bridge driver circuits for each turnout coil
- Uses 4 L298N H bridges for 8 turnouts
- Pin layout designed for adjacent connections with 4-wire dupont connectors
  - Note: One connector needs to be split into 3+1 configuration

### Recommended Hardware Links

- **4-wire Dupont Connectors**: [Amazon Link](https://www.amazon.com/dp/B0CCV3NJ8Q?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_3&th=1)
- **ESP32 Expansion Board**: [Amazon Link](https://www.amazon.com/dp/B0DYDN7LSZ?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_2)
- **Important**: Make sure you get a 32-pin ESP32 if using the above expansion board

## Usage

### Initial Setup

1. Flash the ESP32 with this config using ESPHome
2. Connect to your WiFi and MQTT broker (set credentials in `secrets.yaml`)

### Operation

3. Send MQTT messages to control turnouts:
   - **Topic**: `track/turnout/TO-1-1` (for turnout 1), `track/turnout/TO-1-2` (for turnout 2), etc.
   - **Payload**: `THROWN` or `CLOSED`
4. The ESP32 will pulse the turnout coil for the set time, then turn off

## Customization

### Configuration Options

- **Controller ID**: Change `esp_id` in `substitutions:` to set the controller number
- **Pulse Duration**: Adjust `turnout_pulse_ms` for your turnout hardware
- **Add/Remove Turnouts**: Edit the `mqtt.on_message` and `output` sections

### Example MQTT Commands

```bash
# Throw turnout 1
mosquitto_pub -h your_mqtt_broker -t "track/turnout/TO-1-1" -m "THROWN"

# Close turnout 1
mosquitto_pub -h your_mqtt_broker -t "track/turnout/TO-1-1" -m "CLOSED"
```

## Troubleshooting

### Common Issues

- **Connection Problems**:
  - Ensure your MQTT broker and credentials are correct
  - Verify WiFi network settings in `secrets.yaml`
- **Turnout Not Responding**:
  - Check wiring and pin assignments for each turnout
  - Verify H-bridge connections and power supply
- **Debugging**:
  - Use the ESPHome logs for debugging (set `logger.level: DEBUG`)
  - Monitor MQTT messages to confirm commands are being received

### Pin Assignment Reference

See the `output:` section in `tc-1.yaml` for complete GPIO pin mapping to each turnout's A and B outputs.
