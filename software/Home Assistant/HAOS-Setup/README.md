# 🏠 Stage 1: Home Assistant OS Bare-Metal Installation

This directory manages the initial physical provisioning and bare-metal OS installation for the central **Modular and Open-Source Science Station (MOSSS)** edge gateway.

---

## 📋 Prerequisites & Hardware Checklist

Before beginning, ensure your central hub hardware components match our verified specifications:
*   **Single Board Computer:** Raspberry Pi 4 or Raspberry Pi 5 (Minimum 4GB RAM recommended).
*   **Power Supply:** Official Raspberry Pi USB-C power supply (15W for Pi 4, 27W for Pi 5) to prevent undervoltage failures.
*   **Storage:** A 32GB high-endurance microSD card (UHS Speed Class 3 / V30 or better rated for continuous write cycles) or an external USB 3.0 SSD.
*   **Network:** An Ethernet cable connected directly to your local network switch/router for initial provisioning.

---

## 💿 Installation Step-by-Step

Because the gateway needs to compute vector matrices locally without internet dependence, we utilize the bare-metal **Home Assistant Operating System (HAOS)**.

<Sequence>
{/* Reason: Misordering these setup steps will result in a failed headless boot or network mismatch. */}
  <Step subtitle="Requires Mac, Windows, or Linux PC" title="Download the Flashing Tool">
    Download and install the official **Raspberry Pi Imager** from [raspberrypi.com/software](https://www.raspberrypi.com/software/). Insert your storage media into your flashing computer.
  </Step>
  <Step subtitle="Do not use default Pi OS" title="Select the HAOS Image">
    1. Launch the Imager tool.
    2. Click **Choose Device** and select your model (e.g., Raspberry Pi 5).
    3. Click **Choose OS**, scroll down to select **Other specific-purpose OS**, click **Home Assistant**, and choose **Home Assistant OS**.
  </Step>
  <Step subtitle="Crucial Step" title="Flash without OS Customization">
    Select your target storage device and click **Next**. 
    > ⚠️ **CRITICAL:** If the imager prompts you to apply OS customization settings (like setting up Wi-Fi or SSH), **select NO**. HAOS manages its own network initialization—applying custom configurations through the imager will corrupt the system container structure. Confirm and write the image.
    ![Descriptive Alt Text For Accessibility](./images/Pi-imager.png)
  </Step>
  <Step subtitle="Takes 5-15 minutes" title="Headless Initial Boot">
    Insert the flashed storage into your Raspberry Pi. Connect an **Ethernet cable** to your router, then plug in the power supply. The Pi will boot headlessly; give it up to 15 minutes to automatically provision, unpack the environment, and fetch system dependencies.
  </Step>
  <Step subtitle="Web Browser Setup" title="Complete Onboarding UI">
    On a computer connected to the same local network, open a browser window and navigate to:
    `http://homeassistant.local:8123`
    *(If the hostname fails to resolve, check your router's DHCP client list to find the Pi's IP address and navigate to `http://YOUR_PI_IP:8123`).* Follow the prompts to create your local admin account.
  </Step>
</Sequence>

---

## 🧭 Next Step
Once you have landed on your fresh home assistant dashboard and created your main owner account, advance to user provisioning and system networking:

👉 **Proceed to Stage 2:** [Go to 2-OS-Provisioning](../2-OS-Provisioning/)