# Fortify

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

