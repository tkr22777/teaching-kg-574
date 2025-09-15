## Network Devices in Practice

### What we’ll cover
- NIC, Hub, Switch, Router, Bridge
- Wi‑Fi gear: Wi‑Fi router, WAP, RAP
- Where each device sits in a simple home/office network and what it does


## NIC (Network Interface Card)
- The network port of a device; has a hardware address (MAC) and sends/receives network traffic.
- Tip: To always assign `192.168.10.50` to MAC `AA:BB:CC:DD:EE:FF`, use a router DHCP reservation or set a static IP.


## Hub vs Switch

### Hub (old/repeater)
- Copies anything it hears to all ports. Simple, noisy, not used today.

```mermaid
graph TD
  A[PC A] --- H[Hub]
  B[PC B] --- H
  C[PC C] --- H
  H --- D[PC D]
  A -- copied to everyone --> H
```

### Switch (modern)
- Learns which device is on which port and sends traffic only where needed.

```mermaid
graph LR
  S((Switch))
  A[PC A] --- S --- B[PC B]
  C[PC C] --- S
  A -- directly to B --> S
```

## Bridge
- Like a small 2‑port switch: connects two network segments and forwards useful traffic between them.
- Helps reduce noise between areas and extend networks.

```mermaid
graph LR
  Seg1[Segment A] -- Bridge -- Seg2[Segment B]
```

## Router
- Connects different networks (e.g., your home network to the Internet, or two office segments).
- Chooses a path for traffic between networks; can enforce rules and share one public IP among many devices (home NAT).

```mermaid
graph LR
  LAN[Home/Office Network] --- R[Router] --- Net[Internet]
```

Common in homes: the “Wi‑Fi router” is a router + small switch + wireless access point in one box.

## Wi‑Fi: Router, WAP, RAP

### Wi‑Fi Router
- All‑in‑one box: routes to the Internet, provides a few Ethernet ports, and creates your Wi‑Fi network.

### WAP (Wireless Access Point)
- Adds or extends Wi‑Fi coverage; bridges wireless devices onto your existing wired network.

### RAP (Remote Access Point)
- A WAP that connects back to a main site over the Internet for remote locations.

```mermaid
graph TD
  Phone ~~~ AP((WAP))
  Laptop ~~~ AP
  AP --- Switch
  Switch --- Router
  Router --- Internet
```

---

## Putting it together (simple view)

```mermaid
graph LR
  ISP[Internet] --- GW[Wi‑Fi Router]
  GW --- SW[Switch]
  SW --- PC1[PC]
  SW --- PC2[Printer]
  GW ~~~ Phone[Phone]
```