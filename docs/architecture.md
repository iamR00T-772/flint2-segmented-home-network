# Architecture

The Flint 2 is the Layer-3 gateway, firewall, VPN endpoint, DNS filtering platform, and network storage endpoint all in one device.

## Networks

| VLAN | Network | Purpose |
|---:|---|---|
| 10 | `lan` | Trusted devices / administration |
| 20 | `gaming` | Game consoles |
| 30 | `siem` | Cybersecurity/SIEM lab |
| 40 | `tv` | Smart TVs / streaming |
| 50 | Native IoT | Embedded/IoT devices |
| 60 | Native Guest | Guest Internet access |

VLANs 10–40 are custom networks on the VLAN-aware `br-lan` bridge. IoT and Guest retain GL.iNet's native implementations.

## Ports

WAN is the ISP uplink and does not participate in `br-lan`. LAN1–LAN4 provide untagged access to VLANs 10–40 respectively; LAN5 is unused. On this router, LAN1 can be converted to a second WAN port, but I chose to leave it as a LAN port and use it as a physical administrative port for my main home LAN, in case I need it for future troubleshooting.

## Wireless

The main home LAN, Gaming LAN, SIEM LAN, and TV LAN use the 5 GHz radio frequency. The IoT LAN and Guest LAN use the 2.4 GHz radio frequency.

## Management

LAN1 is a trusted administrative wired-management fallback for VLAN 10. Configuration uses primarily the GL.iNet Admin Panel, as well as the OpenWrt LuCI interface for specific tasks like wireless settings for the custom VLAN architecture.