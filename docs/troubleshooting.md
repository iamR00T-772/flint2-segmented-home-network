# Troubleshooting Timeline

## Clean rebuild

After earlier experiments accumulated unnecessary clutter, artifacts, and complexity, the router was factory-reset and rebuilt around a pre-planned addressing/VLAN scheme.

## VPN policy routing

WireGuard worked successfully under the "All Devices" tunnel source setting, but not for selected VLANs. Route and policy inspection narrowed the failure to source/interface policy selection due to limitations between the GL.iNet/OpenWrt and WireGuard VPN technologies, rather than tunnel establishment itself.

## Smart-TV wireless compatibility

An older Roku TV problem initially resembled DNS-filtering trouble. The actual issue was wireless security compatibility; using a compatible WPA mode enabled connectivity.

## PlayStation wireless compatibility

One PS5 that was intended to join the network via wireless could not join the gaming network under the mixed security mode. WPA2-PSK resolved it.

## AdGuard resource tradeoff

Aggressive filtering increased router's CPU load and operational temperature. The final filtering approach prioritizes useful coverage without unnecessary rule volume and system workload.

## Storage simplification

Earlier partition ideas were abandoned in favor of a single EXT4 Samba disk.

## Reusable troubleshooting order

```text
physical/client connectivity
 -> Wi-Fi authentication / Ethernet
 -> VLAN + DHCP
 -> firewall
 -> DNS/application
 -> routing/policy
 -> WireGuard/WAN
```
