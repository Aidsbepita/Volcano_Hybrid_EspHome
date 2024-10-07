# Volcano Hybrid ESPHome Integration

This project allows you to control and monitor the **Storz & Bickel Volcano Hybrid** vaporizer via an ESP32 board using ESPHome. The ESPHome platform connects the Volcano Hybrid to Home Assistant, enabling remote control and monitoring through BLE (Bluetooth Low Energy).

## Features

- **Monitor Current Temperature**: View the current operating temperature of the Volcano Hybrid.
- **Set Target Temperature**: Adjust the desired temperature of the vaporizer through Home Assistant.
- **Fan Control**: Turn the Volcano fan on and off remotely.
- **Heat Control**: Toggle the heater on and off.
- **LED Brightness Control**: Adjust the brightness of the LED display on the device.

## Prerequisites

Before setting up this project, ensure you have the following:

- **Home Assistant**: A running instance of Home Assistant with Bluetooth capabilities.
- **ESP32 Device**: A compatible ESP32 development board (e.g., ESP32 DevKitC) flashed with ESPHome.
- **Volcano Hybrid**: A Storz & Bickel Volcano Hybrid vaporizer within BLE range.
- **Wi-Fi Network**: Credentials for a Wi-Fi network that the ESP32 device will connect to.

### Requirements

- [ESPHome](https://esphome.io/) installed and configured on the ESP32 board.
- Home Assistant instance with Bluetooth enabled.
- BLE support on Home Assistant or a BLE adapter connected to the Home Assistant server.

## Installation

### Step 1: Clone the Repository

Clone the repository to your local machine or use it as a reference for your own Home Assistant configuration.

```bash
git clone https://github.com/your-repo/volcano_hybrid_esphome.git
cd volcano_hybrid_esphome
```

### Step 2: Flash ESP32 with ESPHome

Make sure ESPHome is installed on your computer. If not, you can install it using Python’s package manager:

```bash
pip install esphome
```

Flash the ESP32 board with the configuration provided in the `volcano_hybrid.yaml` file. This will enable BLE communication between the ESP32 board and the Volcano Hybrid device.

```bash
esphome run volcano_hybrid.yaml
```

### Step 3: Configure Home Assistant

1. In Home Assistant, go to **Configuration > Integrations**.
2. Click the `+` button and search for **ESPHome**.
3. Add your ESP32 device’s IP address to connect it to Home Assistant.
4. Once the device is discovered, you’ll be able to control and monitor the Volcano Hybrid from Home Assistant's dashboard.

### Step 4: Add to Lovelace UI

You can add the Volcano Hybrid entities (fan control, heat control, target temperature, current temperature, LED brightness) to your Home Assistant Lovelace dashboard for easy control:

1. Go to **Overview > Configure UI > Add Card**.
2. Select an appropriate card (e.g., **Entities**, **Button**, or **Slider**).
3. Add the **Volcano Hybrid** entities such as:
   - `switch.volcano_fan`
   - `switch.volcano_heat`
   - `sensor.volcano_current_temperature`
   - `number.volcano_target_temperature`
   - `number.volcano_led_brightness`

### Step 5: Custom Automations (Optional)

You can create custom automations to automate Volcano Hybrid actions (e.g., turning off the heater after reaching a specific temperature). Here's an example automation:

```yaml
alias: Turn off heat when target temperature is reached
trigger:
  platform: numeric_state
  entity_id: sensor.volcano_current_temperature
  above: '200'
action:
  service: switch.turn_off
  entity_id: switch.volcano_heat
```

## Usage

Once set up, you can:

- Monitor the current temperature of your Volcano Hybrid vaporizer in real-time.
- Adjust the target temperature using a slider in Home Assistant.
- Toggle the fan and heater on or off using switches.
- Adjust the LED brightness of the Volcano Hybrid display.

## Troubleshooting

1. **ESP32 not connecting to Wi-Fi**: Ensure the correct Wi-Fi credentials are set in the `yaml` configuration file. Also, ensure the ESP32 is within range of your Wi-Fi network.
2. **BLE connectivity issues**: Make sure the ESP32 device is within BLE range of the Volcano Hybrid vaporizer and that no other devices are actively connected to it via Bluetooth.
3. **Device not responding**: Check the Home Assistant logs for errors or BLE connection issues. If the device is not reachable, try restarting both the ESP32 board and the Home Assistant instance.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
