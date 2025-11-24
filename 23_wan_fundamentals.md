# WAN Fundamentals & Broadband Services

## Overview
Moving beyond the LAN, Week 11 explores the technologies that connect networks across cities, countries, and continents. We'll define the purpose of a Wide Area Network (WAN), examine the physical media and services that underpin them, and introduce the key protocols that enable long-distance communication. The focus is on understanding the conceptual shift from the high-speed, owned infrastructure of a LAN to the slower, carrier-managed world of a WAN.

## Network Types by Scope

```mermaid
graph LR
  PAN["PAN<br/>Personal (1–10 m)"]
  LAN["LAN<br/>Building/Campus (10–1000 m)"]
  MAN["MAN<br/>City/Metro (10–100 km)"]
  WAN["WAN<br/>Country/Global (100+ km)"]

  PAN --> LAN --> MAN --> WAN
```
PANs (Personal Area Networks) are typically short-range (e.g., Bluetooth). LANs cover a single site and are usually organization‑owned. MANs and WANs span cities, countries, or continents and almost always rely on service providers.

## What is a WAN?

### LAN vs. WAN
- **Scope**: LAN (Local Area Network) is a room/building/campus; WAN (Wide Area Network) is geographically dispersed.
- **Ownership**: LANs are typically owned by the organization; WANs utilize public carrier infrastructure.
- **Speed**: LAN speeds are high (1-10 Gbps+); WAN speeds are lower and more expensive.

### Key WAN Terminology
- **Customer Premises Equipment (CPE)**: Devices at the subscriber's location (your router).
- **Demarcation Point (Demarc)**: The point where the carrier's network ends and the customer's network begins.
- **Local Loop**: The "last mile" connection from the provider to the customer.

### WAN Topologies
- **Point-to-Point**: A dedicated link connecting two sites.
- **Hub-and-Spoke**: A central site (hub) connects to multiple branch sites (spokes).
- **Full Mesh**: Every site has a direct connection to every other site (expensive, high-availability).

## WAN Transmission Media

### Revisiting Media in a WAN Context
- **Fiber Optics**: The backbone of all modern WANs and the internet. Used for long-haul, undersea, and high-speed metro connections.
- **Copper (Leased Lines)**: Legacy T1/E1/T3 circuits providing dedicated, symmetric bandwidth. Still used but largely replaced by fiber.
- **Wireless**: Microwave and satellite for remote locations; Cellular (4G/5G) as a primary or backup WAN link.

## Broadband Services

### Connecting to the Internet
A comparison of common "last mile" technologies.

**Comparison Table: Broadband Technologies**

| Technology      | Medium        | Typical Speeds (Down/Up)    | Key Characteristic              |
|-----------------|---------------|-----------------------------|---------------------------------|
| **DSL**         | Copper Phone Line | 5-100 Mbps / 1-20 Mbps      | Distance-sensitive from CO      |
| **Cable**       | Coaxial Cable | 25 Mbps - 1 Gbps / 5-50 Mbps | Shared medium in a neighborhood |
| **Fiber (FTTH)**| Fiber Optics  | 100 Mbps - 10 Gbps (Often Symmetric) | Highest speed and reliability   |
| **Cellular**    | Wireless (RF) | 10-100+ Mbps (Variable)     | Mobility, good for backup       |
| **Satellite**   | Wireless (RF) | 15-100 Mbps (High Latency)  | For remote/rural areas          |

## Quick Review Questions
- What is the primary difference between a LAN and a WAN regarding ownership?
- Why is the "Demarcation Point" important for troubleshooting?
- Which broadband technology is best suited for a remote research station with no wired infrastructure?

