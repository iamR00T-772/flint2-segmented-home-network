# Project Status

**Operational final baseline**

### Deployed
- GL.iNet Flint 2 / GL-MT6000, firmware version 4.9.1
- Custom VLANs 10/20/30/40
- Native GL.iNet IoT/Guest networks as VLANs 50/60, respectively
- Firewall-zone isolation between each VLAN
- WireGuard VPN used by all devices
- UK/Japan/Germany/Australia alternate VPN tunnels for streaming
- AdGuard Home / content filtering
- QoS
- SMB/Samba on a 5 TB EXT4 USB HDD
- GL.iNet Admin Panel + LuCI administration

### Not Deployed
- Per-VLAN WireGuard routing
- Custom replacements for native IoT/Guest
