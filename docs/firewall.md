# Firewall & Isolation

The firewall, not subnetting alone, is what creates the true security boundary.

The isolated Gaming, SIEM, TV, IoT, and Guest zones use restrictive forwarding policies with explicit outbound access. They cannot initiate direct communication with the other internal zones under the final design.

The trusted `lan` zone for VLAN 10 retains administrative privileges for troubleshooting and future configuration changes. Required DHCP/DNS access to the router is explicitly permitted where restrictive input policies would otherwise block it, such as the IoT and Guest zones.

The WAN zone uses masquerading and MSS clamping. Unsolicited inbound access is not part of the design.

The "All Devices" VPN policy changes the outbound internet path and adds "wgclient" zones when a tunnel is enabled, but it does not remove or alter the internal firewall boundaries between VLANs.