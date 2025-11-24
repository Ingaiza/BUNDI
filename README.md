# 🦉 BUNDI: AI-Driven Bio-Acoustic Surveillance

![License](https://img.shields.io/badge/license-MIT-green)
![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![Platform](https://img.shields.io/badge/platform-ROS%202%20Humble-orange)
![Hardware](https://img.shields.io/badge/hardware-ESP32--S3%20%7C%20LoRa-yellow)

**BUNDI** (Swahili for *Owl*) is a scalable, real-time acoustic monitoring network designed to protect the **Kakamega Forest Ecosystem** in Kenya. It uses a network of solar-powered edge devices to detect illegal logging (chainsaws) and poaching activity, relaying alerts to a "Bioluminescent" Command Center via a LoRa Mesh network.

Uniquely, BUNDI integrates a **Blockchain-backed USSD Community Ledger**, allowing local residents to submit anonymous, immutable reports of environmental crimes using basic feature phones.

---

## 📸 Command Center Dashboard

*(Add your screenshots here, e.g., dashboard_main.png)*
> The BUNDI Commander Interface features real-time node tracking, precision threat timelines, and hotspot analysis.

---

## ✨ Key Features

### 1. 🌲 Acoustic Sentry Grid
* **Edge AI:** Runs quantized TFLite models on **ESP32-S3** to classify audio in <200ms.
* **Classes:** Detects `Natural` (Birds/Wind), `Unnatural` (Chainsaws/Vehicles), and `Human` (Voices) sounds.
* **Fire Detection:** Integration with thermal sensors for immediate "CRITICAL" fire alerts.

### 2. 📡 Connectivity & Telemetry
* **LoRa Mesh:** Utilizes SX1278 modules to transmit alerts over 5-15km without cellular coverage.
* **ROS 2 Bridge:** A C++ ROS 2 node bridges the gap between embedded firmware and the cloud dashboard during R&D.

### 3. 🔗 Community Ledger (Blockchain)
* **USSD Interface:** Dial `*384*...#` to report crimes (Logging, Charcoal, Encroachment).
* **Immutability:** Reports are hashed and stored on a local blockchain ledger to prevent data tampering.
* **Anonymity:** Reporter identities are cryptographically masked.

### 4. 📊 Precision Analytics
* **Hotspot Detection:** Algorithms calculate a "Threat Score" to identify the most active illegal zones.
* **Winner-Takes-All Graphing:** Clean visualization that plots only the highest probability class per event.

---

## 🏗️ System Architecture

[Image of IoT data pipeline architecture]

```mermaid
graph TD
    A[ESP32-S3 Node] -->|I2S Mic| B(Audio Capture)
    B -->|TFLite Inference| C{Threat Detected?}
    C -- Yes --> D[LoRa TX]
    C -- No --> E[Deep Sleep]
    D --> F[LoRa Gateway]
    G -->|JSON/HTTP| H[Flask Server]
    
    I[Community User] -->|USSD| J[Africa's Talking API]
    J -->|POST| H
    
    H --> K[Blockchain Ledger]
    H --> L[Command Dashboard]
