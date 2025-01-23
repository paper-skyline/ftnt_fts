# Purpose

There are many different ways to configure FortiTester based on your unique goals and objectives. My goal in creating these example configurations was to familiarize myself with how various network performance and security effectiveness measurements can be configured and utilized based on various bits of examples and pieces of documentation I came across listed below in the Resources section. All of this information is publicly available, I just put some things together that worked for me. 

FortiTester can do some _really_ practical and useful tests that I wish more people knew about, particularly at the price point and deployment models that are available. For example, check out the lists below!

## __Performance Testing__

### Web Related

* HTTP/S CPS Test
* HTTP/S RPS Test
* HTTP/S CC Test
* HTTP/S Throughput Test
* HTTP/2 CPS Test
* HTTP/2 RPS Test
* HTTP/2 CC Test
* HTTP/2 Throughput Test

### VPN Related

* IPSEC Remote Access Test
* IPSEC Remote Access CC Test
* SSL VPN Tunnel CPS Test
* SSL VPN Tunnel RPS Test
* SSL VPN Tunnel CC Test
* SSL VPN Tunnel Throughput Test

### Protocol Specific

* UDP PPS Test
* UDP Payload Test
* UDP Payload Test
* __UDP Protocol DNS Latency Test__
* __UDP Protocol NTP Latency Test__
* UDP Protocol RADIUS Test
* UDP Protocol SIP Test
* UDP Protocol TFTP Test
* __DHCP Test__
* __TCP Throughput Test__
* TurboTCP Test
* TCP Connection Test
* __TCP CIFS/SMB Test__
* TCP Protocol FIX Test
* TCP Protocol FTP Test
* TCP Protocol IMAP Test
* __TCP Protocol LDAP Test__
* TCP Protocol NFS Test
* TCP Protocol POP3 Test
* __TCP Protocol RDP Test__
* TCP Protocol SMTP Test
* __TCP Protocol SSH Test__
* RFC 2544 Throughput Test (Layer 2 test frames)
* RFC 2544 Latency Test (Layer 2 test frames)
* RFC 2544 Loss Rate Test (Layer 2 test frames)
* RFC 2544 Back to Back Test (Layer 2 test frames)
* RFC 3511 IP Throughput Test (Layer 3 packets)
* RFC 3511 Concurrent Capacity Throughput Test (Layer 3 packets)
* IGMP Test
* RTSP/RTP Test
* __Traffic Replay Test__
* GTP Replay Test
* Packet Capture Test
* __Mixed Traffic Test__

### Application Specific

* __Amazon S3__
* AOL Chat (lol)
* BitTorrent
* __DB2__
* Facebook
* Gtalk
* Gmail
* __MSSQL__
* __MySQL__
* Netflix
* Oracle TNS
* PSQL
* Twitter
* __WebEx__
* WhatsApp
* Yahoo Mail
* YouTube

## __Security Testing__

* DDoS Single Packet Flood
* DDoS TCP Session Flood
* DDoS HTTP Session Flood
* DDoS Concurrent Session Flood Test
* DDoS UDP Packet Flood Test
* Fuzzing (invalid IP, TCP, UDP, ICMP)
* IPS Attack Replay
* IPS HTTP Evasion
* Malware Test
* Webcrawler Test
* Web Protection Test

## __ATT&CK Testing__

_FortiTester simulates the actions that a real adversary would do on the clients' systems. It features a Remote Access Tool (RAT) that performs adversary actions on infected hosts and copies itself over the whole network to increase its foothold._

## Examples

1. [FortiTester Kickstart with L2 & L3 RFC tests](./FortiTester%20Kickstart.md)
2. [FortiTester Test Center with Application test](./FortiTester%20Test%20Center.md)
3. [Incorporating Device Under Test (DUT) Monitoring](./Monitoring%20DUT%20-%20Scripting.md)
4. [IPerf Functionality on FortiGates](./IPerf3%20on%20FortiGate.md)

## Resources

* [Fortinet FortiTester](https://www.fortinet.com/products/fortitester)
* [FortiTester Datasheet](https://www.fortinet.com/content/dam/fortinet/assets/data-sheets/FortiTester.pdf)
* [FortiTester Documents](https://docs.fortinet.com/product/fortitester/)

## Disclaimer

__*Use at your own risk*__

These example configurations were a learning tool for me to figure out what works for what I was trying to do, what didn't work, and maybe even a little bit as to why. I make no claims that this is the best way, or even the correct way, to configure devices utilizing this technology. What worked for me in a certain situation may not work for you, etc. I encourage you to take the time to learn and try these things out yourself and make your own judgments.