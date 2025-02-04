# Rate limiting at different layers of the OSI Model 30%

## Application Layer (Layer 7) – API & Web Server Rate Limiting

**Where?** API gateways, web servers (Nginx, Apache), WAF (Web Application Firewall)
**How?** Request-based limiting (e.g., limit 1000 requests per hour per user)

**Techniques:**
- API Key-based limits (e.g., Stripe, AWS APIs)
- User Session or JWT-based limiting
- URL/Endpoint-specific rate limiting
- Rate limiting plugins in Nginx, Apache, or Cloudflare

✅ **Use case**: Prevent API overuse, bot traffic, and web scraping.

##  Transport Layer (Layer 4) – TCP & UDP Rate Limiting
**Where?** Load balancers, firewalls, proxies (e.g., HAProxy, iptables)
**How?** Limit TCP connections per IP or regulate UDP packet rate.

**Techniques:**
TCP SYN flood protection (e.g., Linux sysctl settings)
WebSocket connection limits
UDP request throttling (used in gaming & VoIP)

✅ **Use case:** Prevent too many concurrent TCP connections or UDP packet floods.

##  Network Layer (Layer 3) – IP-Based Rate Limiting
**Where?** Firewalls, routers, cloud network security (AWS Security Groups, Google Cloud Firewall)
**How?** Drop packets or throttle based on source IP.

**Techniques:**
- IP-based rate limiting (e.g., allow only 100 requests/sec per IP)
- DDoS mitigation using edge firewalls (Cloudflare, AWS Shield)
- Ingress/Egress bandwidth throttling

✅ **Use case:** Block abusive IPs, mitigate volumetric DDoS attacks.

## Data Link Layer (Layer 2) – Switch-Level Rate Limiting
**Where?** Network switches, ISP throttling, MAC filtering
**How?** Restrict packet rate per MAC address or enforce bandwidth limits.

**Techniques:**

- Switch port rate limiting (e.g., Cisco QoS settings)
- MAC address filtering (control excessive packet rates)
- ISP traffic shaping (e.g., limit torrent speeds)

✅ **Use case:** Prevent local network congestion, ISP throttling heavy users.

# Strategies to Handle Exceeding Rate Limits
 TODO from CHATGPT
