# Modular and Open-Source Science Station
The Science Station (SS) Topology features a decentralized environmental monitoring network designed for rugged, remote terrain. Utilizing a localized LoRaWAN mesh alongside EcoWitt meteorological sensors, the system aggregates real-time microclimate data, barometric pressure, and physical movement tracking. 

At the core of this infrastructure is the **Wake On Interupt Landslide Detector (WOILD)** subsystem—an open-source hardware and telemetry framework specifically engineered to monitor slope stability and ground acceleration. 

All data streams converge on a centrally located, local Home Assistant Core gateway, which orchestrates automated mobile alerts via custom vector deviation matrices and seamlessly bridges the network into broader smart integrations.
<img src="./ss-topology-image.png" />

## 🛠️ Hardware Stack

| Layer | Device | Sensors / Specs |
| :--- | :--- | :--- |
| **Field Nodes** | Heltec WiFi LoRa 32 V3 | MPU6050 Accelerometer, DHT22, 1W Solar |
| **Weather** | EcoWitt WN90 Array | Piezo Rain, Anemometer, Temp/Humid/Pres |
| **Gateways** | SenseCAP M2 & EcoWitt GW3001 | LoRaWAN (TTN), WiFi |
| **Core Gateway**| Raspberry Pi 4 | 32GB mSD, Home Assistant Core, Nabu Casa |

## 🔄 How It Works (Data Pipeline)
1. **Telemetry Collection:** Solar-powered LoRa nodes monitor environmental metrics and structural movement on the hillsides.
2. **Backhaul:** Data is pushed via LoRaWAN to the SenseCAP gateway (integrated with TTN), while weather data routes through the EcoWitt gateway.
3. **Processing & Action:** Home Assistant Core ingests all streams, handles local logic to control smart infrastructure in the valley, and pushes automated alerts to mobile clients.
