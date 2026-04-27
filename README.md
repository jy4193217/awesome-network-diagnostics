# Awesome Network Diagnostics [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![Maintained by BiuPing](https://img.shields.io/badge/maintained%20by-BiuPing-blue)](https://www.biuping.com)

> A curated list of network diagnostic tools, looking glass services, and troubleshooting guides for sysadmins, SREs, and curious developers.

Whether you're chasing a packet loss in a transcontinental link, debugging a flaky DNS resolution, or just trying to understand why "ping works but the website doesn't load", the right tool can save you hours. This list collects the tools we (the team behind [BiuPing](https://www.biuping.com)) reach for daily, plus the references we wish we'd had earlier in our careers.

## Contents

- [Online Diagnostic Platforms](#online-diagnostic-platforms)
- [Ping & ICMP](#ping--icmp)
- [TCP Port Testing (TCPing)](#tcp-port-testing-tcping)
- [Traceroute & MTR](#traceroute--mtr)
- [DNS Tools](#dns-tools)
- [IP Intelligence & Reputation](#ip-intelligence--reputation)
- [HTTP & Website Performance](#http--website-performance)
- [Looking Glass Services](#looking-glass-services)
- [Command-Line Tools](#command-line-tools)
- [Packet Capture & Analysis](#packet-capture--analysis)
- [Network Monitoring](#network-monitoring)
- [Troubleshooting Guides](#troubleshooting-guides)
- [Books & Learning Resources](#books--learning-resources)
- [RFCs Worth Reading](#rfcs-worth-reading)
- [Contributing](#contributing)

## Online Diagnostic Platforms

Multi-node platforms that run network tests from servers around the world. Useful when you need to confirm an issue isn't local to your ISP.

- [BiuPing](https://www.biuping.com) - Multi-node ping, tcping, traceroute, DNS, and IP reputation. IPv4 and IPv6 dual-stack. Nodes across multiple Chinese ISPs and global locations.
- [ping.pe](https://ping.pe) - Fast multi-location ping and MTR with a clean UI.
- [Ping.eu](https://ping.eu) - Long-running European ping/traceroute service.
- [CA App Synthetic Monitor](https://asm.ca.com/en/checkit.php) - Free public website checker from CA Technologies.
- [GTmetrix](https://gtmetrix.com) - Website performance with waterfall analysis.
- [DNSChecker](https://dnschecker.org) - Global DNS propagation checker.

## Ping & ICMP

The most basic but most-misused tool in the kit. Ping verifies IP reachability and round-trip latency over ICMP — but says nothing about whether your service port is actually accepting connections.

- [iputils ping](https://github.com/iputils/iputils) - The reference Linux implementation.
- [fping](https://github.com/schweikert/fping) - Parallel ping for many hosts at once.
- [hping3](http://www.hping.org/) - Crafted ICMP/TCP/UDP packets for advanced testing.
- [Paping](https://code.google.com/archive/p/paping/) - TCP-flavored ping for Windows.

**Try it online**: [BiuPing Ping](https://www.biuping.com/ping/) (multi-node, IPv4/IPv6)

## TCP Port Testing (TCPing)

When ICMP is filtered or you need to confirm a specific port is reachable, TCP-based reachability tests are essential. They're also the truth-teller when "ping works but the app doesn't".

- [tcping](https://github.com/cloverstd/tcping) - Cross-platform Go implementation.
- [tcping.exe](https://elifulkerson.com/projects/tcping.php) - Classic Windows tcping by Eli Fulkerson.
- [nc / ncat](https://nmap.org/ncat/) - Swiss army knife for TCP/UDP probing.
- [PowerShell Test-NetConnection](https://learn.microsoft.com/en-us/powershell/module/nettcpip/test-netconnection) - Built-in for modern Windows.

**Try it online**: [BiuPing TCPing](https://www.biuping.com/tcping/) (test any port from multiple locations)

## Traceroute & MTR

For locating exactly which hop in a path is dropping packets or adding latency.

- [mtr](https://github.com/traviscross/mtr) - Continuous traceroute with packet loss statistics. The first thing to install on a new server.
- [WinMTR](http://winmtr.net/) - Windows GUI port of mtr.
- [tracepath](https://man7.org/linux/man-pages/man8/tracepath.8.html) - Built-in Linux traceroute alternative, no root required.
- [BestTrace](https://www.ipip.net/product/client.html) - Visual traceroute with ASN annotation, popular in the Chinese-speaking community.
- [PingPlotter](https://www.pingplotter.com/) - Commercial graphical traceroute with historical baselines.

**Try it online**: [BiuPing Traceroute](https://www.biuping.com/traceroute/) (multi-node MTR with hop-by-hop loss)

## DNS Tools

- [dig](https://www.isc.org/bind/) - The canonical DNS query tool, ships with BIND.
- [drill](https://nlnetlabs.nl/projects/ldns/about/) - dig alternative, more concise output.
- [dnsutils](https://gitlab.isc.org/isc-projects/bind9) - host, nslookup, dig as a bundle.
- [DNSViz](https://dnsviz.net/) - DNSSEC chain visualization.
- [DNSChecker](https://dnschecker.org/) - Global propagation testing across resolvers.
- [Public DNS Resolvers](https://github.com/curl/curl/wiki/DNS-over-HTTPS) - Reference list of trustworthy resolvers.

**Try it online**: [BiuPing DNS Lookup](https://www.biuping.com/dns/) (cross-region propagation check)

## IP Intelligence & Reputation

Identifying whether an IP is residential, datacenter, proxy, VPN, or Tor exit — and whether it's been flagged for abuse.

- [AbuseIPDB](https://www.abuseipdb.com/) - Open community IP abuse database.
- [Spamhaus](https://www.spamhaus.org/) - Authoritative blocklists for email and threat intelligence.
- [IPinfo](https://ipinfo.io/) - Commercial IP geolocation and ASN data with a generous free tier.
- [MaxMind GeoLite2](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data) - Free geolocation database.
- [Team Cymru IP-to-ASN](https://team-cymru.com/community-services/ip-asn-mapping/) - Free ASN lookup service.
- [BGP.tools](https://bgp.tools/) - Public BGP routing table exploration.

**Try it online**: [BiuPing IP Reputation](https://www.biuping.com/ip_reputation/) (proxy/VPN/datacenter detection with risk scoring)

## HTTP & Website Performance

- [curl](https://curl.se/) - The internet's universal HTTP client.
- [httpie](https://httpie.io/) - Friendlier curl with JSON-aware output.
- [WebPageTest](https://www.webpagetest.org/) - In-depth waterfall analysis.
- [Lighthouse](https://github.com/GoogleChrome/lighthouse) - Google's automated auditing tool.

**Try it online**: [BiuPing Website Speed Test](https://www.biuping.com/http/) (DNS/TCP/TLS/TTFB waterfall from multiple regions)

## Looking Glass Services

Read-only access to BGP routers operated by ISPs and IXPs. Indispensable for cross-AS routing investigations.

- [HE.net Looking Glass](https://lg.he.net/) - Hurricane Electric's classic.
- [NTT Looking Glass](https://www.gin.ntt.net/looking-glass/)
- [Cogent Looking Glass](https://www.cogentco.com/en/looking-glass)
- [traceroute.org](http://traceroute.org/) - Directory of public looking glass servers worldwide.

## Command-Line Tools

- [ss](https://man7.org/linux/man-pages/man8/ss.8.html) - Modern replacement for netstat.
- [iperf3](https://github.com/esnet/iperf) - TCP/UDP bandwidth measurement.
- [nmap](https://nmap.org/) - Port scanning and service detection.
- [tcptraceroute](http://michael.toren.net/code/tcptraceroute/) - Traceroute over TCP, gets through ICMP-filtered networks.
- [arp-scan](https://github.com/royhills/arp-scan) - L2 host discovery.
- [scapy](https://scapy.net/) - Python-based packet crafting library.

## Packet Capture & Analysis

- [Wireshark](https://www.wireshark.org/) - The reference packet analyzer.
- [tcpdump](https://www.tcpdump.org/) - Command-line capture, runs anywhere.
- [tshark](https://www.wireshark.org/docs/man-pages/tshark.html) - Wireshark's CLI sibling.
- [termshark](https://termshark.io/) - Terminal UI for tshark.
- [PacketTotal](https://packettotal.com/) - PCAP file analysis service.

## Network Monitoring

- [SmokePing](https://oss.oetiker.ch/smokeping/) - Long-term latency baseline tracking.
- [Prometheus blackbox_exporter](https://github.com/prometheus/blackbox_exporter) - HTTP/TCP/ICMP probing for Prometheus.
- [Zabbix](https://www.zabbix.com/) - Full-stack monitoring with strong network features.
- [LibreNMS](https://www.librenms.org/) - SNMP-based network monitoring.

## Troubleshooting Guides

Symptom-driven guides for common network issues.

- [BiuPing: Why a webpage loads slowly — a 5-step diagnosis](https://www.biuping.com/article/15)
- [BiuPing: Ping works but the website won't load — 7 common causes](https://www.biuping.com/article/14)
- [BiuPing: How to read MTR output and locate cross-network congestion](https://www.biuping.com/article/11)
- [BiuPing: What is acceptable packet loss?](https://www.biuping.com/article/12)
- [BiuPing: Differences between Ping and TCPing](https://www.biuping.com/article/6)
- [Cloudflare Learning: How a DNS query works](https://www.cloudflare.com/learning/dns/what-is-dns/)
- [Julia Evans: How DNS works (zine)](https://wizardzines.com/zines/dns/)

## Books & Learning Resources

- *TCP/IP Illustrated, Vol. 1* by W. Richard Stevens — The foundation.
- *Computer Networking: A Top-Down Approach* by Kurose & Ross — Best academic intro.
- *High Performance Browser Networking* by Ilya Grigorik — [Free online](https://hpbn.co/).
- *BPF Performance Tools* by Brendan Gregg — Modern observability deep-dive.

## RFCs Worth Reading

- [RFC 792](https://tools.ietf.org/html/rfc792) - ICMP
- [RFC 793](https://tools.ietf.org/html/rfc793) - TCP
- [RFC 1035](https://tools.ietf.org/html/rfc1035) - DNS
- [RFC 4787](https://tools.ietf.org/html/rfc4787) - NAT behavior requirements

## Contributing

Pull requests welcome. Please follow these guidelines:

- One tool per line, alphabetically within each section.
- Include a short, factual description (1 sentence).
- Tools must be actively maintained (last commit/release within 12 months for open source).
- No affiliate links. Commercial tools are fine if they offer a meaningful free tier.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

[![CC0](https://img.shields.io/badge/license-CC0--1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is maintained by the team at [BiuPing](https://www.biuping.com). To the extent possible under law, contributors have waived all copyright and related rights.
