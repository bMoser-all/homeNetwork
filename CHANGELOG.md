# Router Configuration Changelog

MikroTik Chateau 5G R17 ax — configuration version history.

---

## V5 — 2026-04-02 *(current)*

**First version tracked in Git.** Summary based on binary backup analysis.

### Network Topology
- **WAN**: Quectel RG650E-EU 5G NR Sub-6GHz module via `lte1`
- **Main LAN bridge** (`bridge`) — primary network for trusted devices
- **Diver bridge** (`bridge-diver`) — isolated segment for IoT/guest devices
  - VLAN 10 (`vlan10-diver`) tags diver traffic on the trunk
  - Separate NAT masquerade rule (`diver NAT`) for internet access
  - No layer-2 access to main LAN (full isolation)

### Wi-Fi
| Interface | Radio | SSID | Network |
|-----------|-------|------|---------|
| `wifi1` / `wifi10` | 5 GHz / 2.4 GHz | `audiopro` | Main LAN |
| `wifi2` / `wifi20` | 5 GHz / 2.4 GHz | `diver` | Diver (IoT/guest) |

### Firewall Highlights
- Standard `defconf` input/forward/srcnat chains
- **mDNS bridging** rules forward multicast between `bridge` and `bridge-diver` (enables Chromecast discovery etc.)
- IPv4 + IPv6 filter sets (drop invalid, accept established/related, fasttrack)

### VPN
- **WireGuard** interface (`iface-wireguard`) configured

### DHCP Static Leases
| Hostname | Device |
|----------|--------|
| `DiskStation` | Synology DS218+ NAS |
| `Mac` | macOS computer |
| `Pixel-8` | Google Pixel 8 |
| `iPhone` | Apple iPhone |
| `Galaxy-A71` | Samsung Galaxy A71 |
| `audiocast` | Chromecast / audio streamer |

---

<!-- Add new versions above this line, oldest at the bottom -->
