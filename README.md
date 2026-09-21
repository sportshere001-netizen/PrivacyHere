# PrivacyHere 🛡️

PrivacyHere is a 100% offline, open-source Android hardware kill switch. It leverages Android's native Enterprise `DevicePolicyManager` to physically sever hardware components at the kernel level, ensuring absolute privacy from third-party apps, trackers, and the OS itself.

## 🔒 Core Architecture
Unlike standard privacy apps that rely on background services or Accessibility overlays (which can be bypassed or killed by the OS), PrivacyHere runs as an **Immutable Device Owner**. 

* **Camera:** Severed via `DevicePolicyManager.setCameraDisabled()`. Disables the Camera Hardware Abstraction Layer (HAL) globally.
* **Microphone:** Blocked via `UserManager.DISALLOW_UNMUTE_MICROPHONE`. Forces the OS audio router to drop all mic requests.
* **Motion Sensors:** Locked via Android's native `sensor_privacy` secure settings flag (disables Gyroscope, Accelerometer, and Ambient Light sensors).
* **Zero Telemetry:** The `AndroidManifest.xml` strictly forbids internet access. The app cannot ping external servers.

## ⚠️ Installation (Enterprise QR Provisioning)
Because OEM security daemons (like Xiaomi's Security Center and Samsung Knox) actively block standard ADB Device Owner assignments, this app **requires a Factory Reset** to install properly via Google's official CTS-mandated backdoor.

1. Factory reset your Android device.
2. On the initial "Hello / Welcome" setup screen, tap the empty space **6 times**.
3. Connect to Wi-Fi and scan the PrivacyHere Enterprise Provisioning QR Code.
4. The OS will download the APK, verify its SHA-256 checksum, and statically compile it as the Device Owner before OEM security daemons can boot.

## ⚖️ Legal Disclaimer
**Provided AS-IS.** By installing this software, you assume all responsibility for your device's configuration. The developers accept absolutely zero liability for missed alarms, disabled phone calls, system instability, or data loss resulting from severing hardware access. 

---
*License: MIT*
