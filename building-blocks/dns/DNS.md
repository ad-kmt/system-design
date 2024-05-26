# Domain Name System (DNS)

## Introduction
The Domain Name System (DNS) is a hierarchical and decentralized naming system used to translate human-readable domain names into IP addresses. This system allows humans to use memorable names like `google.com` instead of numeric IP addresses such as `122.250.192.232`.

## How DNS Works
DNS lookup involves several steps:

1. A client types a domain name (e.g., `example.com`) into a web browser.
2. The query is sent to a DNS resolver.
3. The resolver queries a DNS root nameserver.
4. The root server responds with the address of a Top-Level Domain (TLD) server.
5. The resolver requests the IP address from the TLD server.
6. The TLD server provides the IP address of the domain's nameserver.
7. The resolver queries the domain's nameserver.
8. The nameserver returns the IP address to the resolver, which then sends it to the web browser.

![](https://github.com/donnemartin/system-design-primer/raw/master/images/IOyLj4i.jpg)



## DNS Server Types

### DNS Resolver
- **Managed by**: Internet Service Providers (ISPs) or private organizations.
- **Example**: Google's public DNS resolver at `8.8.8.8`.
- **Function**: Acts as the middleman between a client and DNS nameservers. Queries root nameservers, TLD nameservers, and authoritative nameservers. Provides responses from cache or new queries.

### DNS Root Server
- **Managed by**: Internet Corporation for Assigned Names and Numbers (ICANN).
- **Example**: The root server managed by Verisign.
- **Function**: Accepts queries from recursive resolvers. Directs the resolver to the appropriate TLD nameserver. There are 13 types of root nameservers distributed globally using Anycast routing.

### TLD Nameserver
- **Managed by**: Internet Assigned Numbers Authority (IANA), a branch of ICANN.
- **Example**: The `.com` TLD nameservers managed by Verisign.
- **Function**: Manages information for domain names sharing a common extension (e.g., .com, .net). Divided into generic TLDs (e.g., .com, .org) and country code TLDs (e.g., .uk, .us).

### Authoritative DNS Server
- **Managed by**: Domain name owners or third-party DNS hosting providers.
- **Example**: Authoritative nameserver for `example.com` managed by Cloudflare.
- **Function**: Provides the IP address for a specific domain. Final step in the DNS resolution process. Returns A records (IP addresses) or CNAME records (aliases).

## How it works with Route 53 Managed DNS by AWS

![](https://i2.wp.com/blog.knoldus.com/wp-content/uploads/2019/04/route53.png?fit=640%2C351&ssl=1)

![](https://d1.awsstatic.com/Route53/product-page-diagram_Amazon-Route-53_HIW%402x.4c2af00405a0825f83fca113352b480b19d9210e.png)


## DNS Query Types

### Recursive Query
- DNS client expects a full response or an error.
- Typically handled by a DNS resolver.

### Iterative Query
- DNS client receives the best answer available.
- May be referred to other servers if necessary.

### Non-recursive Query
- DNS resolver returns a cached or authoritative answer immediately.
- No additional queries needed.

## DNS Record Types
- **A (Address Record)**: Holds the IP address of a domain.
- **AAAA (IPv6 Address Record)**: Holds the IPv6 address of a domain.
- **CNAME (Canonical Name Record)**: Forwards one domain to another.
- **MX (Mail Exchanger Record)**: Directs mail to an email server.
- **TXT (Text Record)**: Stores text notes, often used for email security.
- **NS (Name Server Record)**: Stores the name server for a DNS entry.
- **SOA (Start of Authority)**: Stores administrative information about a domain.
- **SRV (Service Location Record)**: Specifies a port for services.
- **PTR (Pointer Record)**: Provides a domain name for reverse lookups.
- **CERT (Certificate Record)**: Stores public key certificates.

## Subdomains
Subdomains are additional parts of the main domain, used to separate sections of a website. For example, `blog.example.com` is a subdomain of `example.com`.

## DNS Zones
A DNS zone is a portion of the domain namespace managed by an entity, allowing granular control over DNS components like authoritative name servers.

## DNS Caching
DNS caching stores records temporarily to speed up subsequent lookups. Each record has a time-to-live (TTL) indicating how long it can be cached.

## Reverse DNS
Reverse DNS lookup resolves an IP address to a domain name using PTR records. Commonly used by email servers to verify the legitimacy of messages.

## Examples of Managed DNS Solutions
- Route53
- Cloudflare DNS
- Google Cloud DNS
- Azure DNS
- NS1

## What Next?
### Related Topics
- DNS Security Extensions (DNSSEC)
- Dynamic DNS (DDNS)

### Topics for Deeper Understanding
- In-depth functioning of DNS resolvers
- DNS zone transfers and updates
- DNS load balancing and failover mechanisms
