# Love Lamps — Device Configuration Hub

This repository serves as the centralized static hosting infrastructure for **Love Lamps** IoT devices. It provides remote configuration, feature flags, and Over-The-Air (OTA) firmware updates.

The infrastructure is hosted via **GitHub Pages** to ensure high availability and low latency globally.

## 📡 Service Endpoints

| Resource | Endpoint URL                              | Description |
| :--- |:------------------------------------------| :--- |
| **Main Config** | `https://ota.lovelamps.name/config.json`  | JSON configuration fetched by devices on boot. |
| **Firmware** | `https://ota.lovelamps.name/firmware/` | Directory containing versioned binary files (`.bin`). |

## ⚙️ Configuration Structure (`config.json`)

The device configuration file adheres to the following JSON schema:

```json
{
  "meta": {
    "updated_at": "ISO 8601 Timestamp",
    "message": "Admin notes or user-facing motd"
  },
  "system": {
    "min_allowable_version": "1.0.0",
    "maintenance_mode": false
  },
  "mqtt": {
    "broker": "broker-address.example.com",
    "port": 8883,
    "use_ssl": true
  },
  "firmware": {
    "latest_version": "1.0.0",
    "url": "https://ota.lovelamps.name/firmware/fw_v1.0.0.bin",
    "force_update": false
  }
}
```

## 🚀 Deployment Workflow
To update the configuration for the device fleet:
1. Modify config.json in the main branch.
2. Commit and push the changes:
```bash
git commit -am "chore: update mqtt broker address"
git push origin main
```
3. GitHub Actions (Pages) will automatically deploy the changes.
4. Propagation time: Updates typically propagate within 60 seconds. Devices will pick up the new config upon their next reboot or scheduled sync.

## ⚠️ Security Notice
- This repository is **PUBLIC**.
- **DO NOT** store sensitive credentials (passwords, private keys, tokens) in this repository.
- Only public endpoints and non-sensitive configuration parameters should be hosted here.

---

© 2026 Love Lamps Team. All rights reserved.
