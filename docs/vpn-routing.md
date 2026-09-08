# WireGuard VPN Routing

## Final State

The router uses an **All Devices** WireGuard policy. One tunnel is active at a time, with a primary U.S. tunnel and UK, Japan, Germany, and Australia alternatives for media streaming purposes from other regions.

## Failed Per-VLAN Experiment

VLAN-specific source VPN routing was investigated but did not become functional due to limitations with how the GL.iNet VPN policy manager handled my custom VLAN segmentation.

`ip route get 1.1.1.1` showed the ISP path during failed policy tests, while inspection of `TUNNEL8220_ROUTE_POLICY` exposed stale/invalid interface state represented as `noneif`.

This demonstrated that a working WireGuard tunnel and correct policy routing are two separate problems.

```text
client -> source interface -> policy/mark -> routing table -> WireGuard -> internet
```

The final build intentionally uses the stable "All Devices" model. When region switching is necessary, the primary tunnel is disabled and the selected regional "All Devices" tunnel is activated.