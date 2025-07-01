# ESPHome Servo Turnout Control (tc-servo.yaml)

## Overview

This configuration controls model railroad turnouts using RC servos on an ESP32. Each turnout is controlled by a servo, with MQTT switches for automation and Home Assistant controls for calibration and monitoring.

## How it Works

- Each turnout has a servo connected to a GPIO pin (see `output:` and `servo:` sections for mapping).
- Turnouts are controlled via MQTT switches (for JMRI or automation) and can be calibrated using Home Assistant (slider and buttons).
- Max and min angles are saved to flash and can be set from Home Assistant.
- Sensors expose the current, max, and min angle for each turnout to Home Assistant.

## Hardware Setup

- ESP32 (32-pin recommended)
- RC servos connected to recommended GPIO pins (see YAML comments)
- Power supply capable of handling servo current

## Usage

1. Flash the ESP32 with this config using ESPHome.
2. Connect to your WiFi and MQTT broker (set credentials in `secrets.yaml`).
3. Use MQTT to throw/close turnouts (see switch section for topics).
4. Use Home Assistant to calibrate and monitor angles (slider and buttons).

## Customization

- Change `controller_num` and `num_turnouts` in `substitutions:` to set the controller and number of turnouts.
- Add more turnouts by duplicating the relevant blocks in `globals`, `output`, `servo`, `switch`, `number`, `button`, and `sensor` sections.
- Adjust servo min/max levels if needed for your hardware.

## Troubleshooting

- If servos hum, the config detaches PWM after movement to reduce noise.
- Ensure your MQTT broker and credentials are correct.
- Check wiring and pin assignments for each servo.
- Use the ESPHome logs for debugging.
