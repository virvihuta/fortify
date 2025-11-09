# Fortify

![Python](https://img.shields.io/badge/python-3.10+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-prototype-yellow.svg)

Fortify is a lightweight, fully local cybersecurity prototype that **discovers devices on your network**, **analyzes their behavior using AI** and **protects you from potential threats in real time** — all from your laptop, with **no cloud dependencies**.

## Overview

Fortify acts as a **mini network security agent** for your home or demo environment.  
It continuously monitors traffic metadata, learns normal device behavior and identifies anomalies that may signal risk — visualizing everything through a modern **Dashboard**.

## How It Works

1. **Device Discovery**  
   - Uses ARP or Nmap to scan your local network.  
   - Maps MAC address prefixes to vendor names via an OUI database.  
   - Builds a live device inventory (IP, MAC, Vendor, Type).  

2. **Traffic Capture**  
   - Captures only metadata (not payloads) using **Scapy** or **PyShark**.  
   - Records metrics like byte counts, DNS lookups and connection rates.  

3. **Feature Aggregation**  
   - Groups observations into 1-minute windows per device.  
   - Stores summaries in a CSV for later model training or replay.  

4. **Anomaly Detection**  
   - Trains an **Isolation Forest** using your normal network data.  
   - Scores each device in real time and flags outliers as risky.  

5. **Frontend Visualization**  
   - The Python backend streams device stats and risk scores via a local API.  
   - The Dashboard consumes this data, visualizing:
     - Live device table  
     - Historical charts  
     - Active alerts  

6. **Protection Actions**  
   - Executes basic firewall rules for risky destinations.  
   - Confirms action results and logs them for traceability.  

## Tech Stack
- **Python 3**
- **Scapy / PyShark** – for packet capture
- **Pandas / NumPy** – for data aggregation
- **Scikit-learn & Pytorch** – for anomaly detection (Isolation Forest / Neural Network)
- **Flask** – to expose data API endpoints
- **React** – for dashboard UI

## Development Plan

### Week 1-2: Foundation
**Hasanaj:** Device discovery (ARP scan) + packet capture (scapy) → output metadata JSON  
**Virvi:** Research features, load sample PCAPs, design feature schema (15-20 features)  
**Mjeda:** Flask setup, basic dashboard UI, device table with fake data  
**Integration:** Discovery → Dashboard shows real devices

### Week 3-4: Feature Pipeline & First Model
**Hasanaj:** Time-window aggregation (5-min windows per device), DNS logging, connection tracking  
**Virvi:** Feature extraction pipeline, train Isolation Forest on 24h baseline, output risk scores (0-100)  
**Mjeda:** Activity charts, risk score display (color-coded), alerts panel  
**Integration:** Capture → Features → ML Scoring → Dashboard with live risk

### Week 5-6: Rule Engine & Polish
**Hasanaj:** Rule-based detection (traffic spikes, port scans, DNS anomalies), threat intel blocklists  
**Virvi:** Combine ML + rules, per-device baselines, explainability (top reasons for alerts)  
**Mjeda:** Alert filtering, WebSocket updates, settings page (adjust thresholds), charts (traffic/risk/protocols)  
**Integration:** ML + Rules → Combined alerts with explanations

### Week 7-8: Protection & Testing
**Hasanaj:** Firewall integration (block/unblock IPs), cross-platform support, stress testing  
**Virvi:** Auto-response logic, false positive tracking, model tuning, unit tests  
**Mjeda:** Block/unblock UI, protection logs, error handling, loading states  
**Integration:** Full system 24h test, bug fixes

### Week 9-10: Demo Mode & Documentation
**Hasanaj:** Packet replay tool, demo scenarios (normal/suspicious/attack PCAPs)  
**Virvi:** Synthetic attack data, replay mode, presentation notebooks  
**Mjeda:** Demo mode toggle, playback controls, scenario selector, export (CSV/PDF)  
**All:** Write documentation (technical, user guide, installation), create video tutorial

### Week 11-12: Final Integration & Conference Prep
**Week 11:** Integration testing, 48h continuous run, bug fixes, code cleanup, polish UI  
**Week 12:** Presentation slides, demo script, rehearsals, backup materials (video/slides)  
**Demo Day:** 10-min live demo (discovery → detection → alert → block → replay)

### Key Milestones
- **Week 2:** Live device table updating  
- **Week 4:** Risk scores displayed, first ML detection  
- **Week 6:** Rule alerts working, polished dashboard  
- **Week 8:** Full system stable (v0.3)  
- **Week 10:** Demo mode ready (v0.9)  
- **Week 12:** Conference ready (v1.0)

### Weekly Cadence
- **Monday 6pm:** Planning sync (30 min)  
- **Friday 6pm:** Integration demo (30 min)  
- **Daily:** 5-min standup on Discord (async)  
- **Integration points:** End of Week 2, 4, 6, 8, 10

### Success Criteria
- Discovers all devices <30 sec  
- Detects simulated attacks <5% false positive rate  
- Dashboard loads <2 sec, real-time updates  
- 10-min live demo runs flawlessly  
- Works on Linux + macOS  
- Complete documentation + video tutorial

## Use Cases

- **Home Network Security:** Monitor your personal devices for suspicious behavior
- **IoT Device Auditing:** Discover what your smart home devices are really doing
- **Security Education:** Learn about network traffic analysis and ML-based detection
- **Conference Demos:** Showcase real-time threat detection in a controlled environment
- **Research Prototype:** Foundation for academic network security research

## Contributing

This is an educational prototype built by:
- **Virvi Huta** – Data Science & ML
- **Aiden Hasanaj** – Network Security & Capture
- **Aiden Mjeda** – Full-Stack & Dashboard

Contributions welcome! Please open issues or PRs.

## Requirements

- Python 3.10+
- Linux or macOS (Windows support experimental)
- Root/sudo access (for packet capture)
- 4GB+ RAM recommended
- WiFi or Ethernet connection to local network


## Limitations

- **Home Network Scale:** Designed for 5-50 devices, not enterprise-scale
- **False Positives:** IoT devices may trigger alerts due to unusual behavior patterns
- **Detection Delay:** 5-minute windows mean attacks aren't detected instantly
- **No Deep Packet Inspection:** Cannot analyze encrypted payload content
- **Platform Support:** Best on Linux, macOS support good, Windows experimental

## Landing Page
[https://fortify-platform.com](https://fortify-platform.com)
[![Netlify Status](https://api.netlify.com/api/v1/badges/db03471a-caa0-48c5-8745-b391f4e2fb3f/deploy-status)](https://app.netlify.com/projects/fortify-platform/deploys)

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE) — free to use, learn from, and extend.

**Disclaimer:** Fortify is a prototype for educational and demonstration purposes. Not intended for production security use. Always comply with local laws regarding network monitoring.
