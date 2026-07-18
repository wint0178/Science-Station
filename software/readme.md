# 💻 MOSSS Software & Configuration Deployment Guide

This directory contains the core software components, custom firmware, and automation logic that power the network topology of the **Modular and Open-Source Science Station (MOSSS)**. 

The software ecosystem is split into three modular pillars: **Long-Range Telemetry Nodes**, **Encrypted Remote I/O Links**, and **Central Gateway Orchestration**.

---

## 📂 Directory Structure

*   **`./Landslide-Detectors/`**: Contains the firmware sketches, hardware interrupt configurations, and payload decoders for the primary, field-deployed **WOILD v1.1.3** (Wake on Interrupt Landslide Detector) LoRaWAN arrays.
*   **`./ESPHome/`**: Contains production-ready YAML firmware templates (`esphome-tailscale.yaml`) that compile specialized Tailscale client binaries directly onto remote ESP32-S3 boards to tunnel encrypted telemetry over Wi-Fi without firewall modifications.
*   **`./Home-Assistant/`**: Contains the central operating system guidelines, multi-tiered user privileges, custom template sensors, and data-logging optimizations required to process field inputs locally.

---

## 🛠️ Step-by-Step Implementation

To deploy this integrated environmental intelligence package on your own network infrastructure, execute these configuration steps sequentially:

### Step 1: Flash the WOILD Hardware Nodes
1. Navigate to the `./Landslide-Detectors/` folder.
2. Open the primary `.ino` sketch file in the **Arduino IDE** (ensure you have installed the core microcontroller board definitions).
3. Configure your unique local network parameters (LoRaWAN APP EUI / NWK KEY) within the top configuration block.
4. Compile and flash the firmware. 
    > 💡 *Note: The firmware utilizes hardware interrupt mapping to keep the MCU in a deep-sleep state under normal operating constraints—transmitting baseline telemetry every 60 minutes to minimize storage writes and maximize battery life.*

### Step 2: Provision Your Remote ESP32/ESPHome Devices (Optional)
1. Navigate to the `./ESPHome/` folder.
2. Open `esphome-tailscale.yaml` and update your `device_id`, generating a unique Base64 API key and fresh Tailscale auth token.
3. Compile and flash your ESP32-S3 boards. On boot, these chips build an internal, encrypted WireGuard tunnel over the local Wi-Fi, joining your private network mesh to feed data streams securely across cellular or distant relays.

### Step 3: Configure the Home Assistant Gateway
1. Navigate to the `./Home-Assistant/` folder and review the installation guide to provision **Home Assistant OS (HAOS)** on a Raspberry Pi 4 or 5 using a 32GB high-endurance microSD card.
2. Create your multi-tiered user profile layout under **Settings > People**. Ensure you create a dedicated Machine-to-Machine (M2M) profile called `databroker` (login: `databroker`) to handle incoming data streams securely.
3. Configure your local **Recorder** filter component using the provided template to restrict data-logging to your strict 30-day target, protecting your SD card from excessive write wear.
4. Copy the custom template sensors into your local `configuration.yaml` file to process raw payloads into the live **2D Vector Deviation Matrix**.

### Step 4: Map Inputs to Your Meteorological Sensors
1. Ensure your local **EcoWitt** weather gateway is integrated with Home Assistant, calibrated to transmit wind, rain, and pressure data updates at a steady **5-minute ingestion cadence**.
2. Optional: Embed interactive meteorological vector models directly onto your UI dashboard using a standard Webpage Card pointing to a customized Windy.com viewport string.

---

## 🔔 How the Alert Logic Works

Once deployed, the software relies on a dual-trigger mechanism to completely eliminate false alerts from environmental noise (like high wind vectors or passing animals):

1. **The Wake-on-Interrupt Event:** The physical landslide tracking node remains completely silent in deep sleep until an active geometric slope threshold is crossed, waking up instantly to blast a high-priority telemetry payload to the gateway via LoRaWAN or ESPHome.
2. **The Vector Deviation Matrix Evaluation:** Home Assistant intercepts the payload using the `databroker` channel, runs it through internal matrix template equations, evaluates the concurrent localized rain accumulation rate from your EcoWitt array, and instantly fires a high-priority mobile notification through the Home Assistant Companion App if both thresholds match critical slope-failure parameters.