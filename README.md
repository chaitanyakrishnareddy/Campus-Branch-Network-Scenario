Campus–Branch Network Scenario: Inter-VLAN + EIGRP + PAT

Hands-on Cisco Packet Tracer scenario for a main Campus (HQ) and a Branch. You’ll segment users with VLANs, route between VLANs using router-on-a-stick, run EIGRP (AS 100) between sites, and centralize Internet at HQ with PAT. DHCP is provided by a server at each site with helpers on the router subinterfaces.

---

Scenario

- HQ: Sales (VLAN 10), HR+IT (VLAN 30), ServerNet (VLAN 20 → DHCP server lives here)
- Branch: Sales (VLAN 40), Guest (VLAN 50)
- Routing: EIGRP 100 with fast timers (hello 5 / hold 15)
- Internet: Centralized at HQ (PAT on HQ’s S0/0/1 to 203.0.113.2)
- DHCP: One server per site; per-VLAN pools; DNS 8.8.8.8
- Security (optional): Guest VLAN cannot reach corporate subnets

---

## Addressing

| Segment                | VLAN | Gateway        | Subnet             |
|------------------------|-----:|----------------|--------------------|
| HQ Sales               | 10   | 192.168.10.1   | 192.168.10.0/24    |
| HQ HR+IT               | 30   | 192.168.30.1   | 192.168.30.0/24    |
| HQ ServerNet (DHCP)    | 20   | 192.168.20.1   | 192.168.20.0/24    |
| Branch Sales           | 40   | 192.168.40.1   | 192.168.40.0/24    |
| Branch Guest           | 50   | 192.168.50.1   | 192.168.50.0/24    |
| WAN HQ↔Branch          |  —   | 10.0.0.1/2     | 10.0.0.0/30        |
| ISP PtP (HQ outside)   |  —   | 203.0.113.1/2  | 203.0.113.0/30     |
| Test DNS (ISP loopback)|  —   | 8.8.8.8        | 8.8.8.8/32         |

DNS for clients: 8.8.8.8


