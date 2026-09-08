# VLAN Design

The addressing convention maps VLAN IDs to the third IPv4 octet in a simple and traditional manner:

```text
10 -> 10.10.10.0/24
20 -> 10.10.20.0/24
30 -> 10.10.30.0/24
40 -> 10.10.40.0/24
50 -> 10.10.50.0/24
60 -> 10.10.60.0/24
```

These networks separate devices by their function and level of trust: trusted home networking, gaming, security experimentation, entertainment, IoT, and guests.

An earlier plan treated all six as custom VLANs. The final build uses custom VLANs 10–40 while retaining GL.iNet's native IoT and Guest networks for 50/60 for simplicity and convenience, while still isolating these devices on their own appropriate networks.
