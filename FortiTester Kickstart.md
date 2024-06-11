# FortiTester Kickstart

[Detailed list of FortiTester Functions](https://docs.fortinet.com/document/fortitester/7.4.1/administration-guide/839782/features-and-benefits)
[FortiTester Admin Guide](https://docs.fortinet.com/document/fortitester/7.4.1/administration-guide/452052/introduction)

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

## Setup Instructions

1. Unbox, rack, and power-on the appliance
2. Connect the MGMT port to a laptop on the 192.168.1.0/24 network
    * Default address of the FTS appliance is https://192.168.1.99
    * Default username is 'admin' with no password, it will prompt you to create a password after first login
3. Connect the console port to your normal Out of Band (OOB) solution like a Lantronix or OpenGear Console Server
    * Default console port settings are 9600/8/N/1/None
4. From the Status Dashboard, we're going to change:
    * Hostname
    * System Timezone and NTP Settings
5. `Network > Interface` to set either a static IP or DHCP
    * Under DNS, either go with the defaults (FortiGuard) or change them to internal DNS servers
6. Logout, re-cable the MGMT interface to your production management network, and log back into the device
7. `System > Setting` to review and possibly increase the 'Idle Timeout' and change the appliance GUI certificate
8. `System > FortiGuard` to update the firmware to the current version 7.4.1
9. `Log & Report` to configure a syslog server if you want FTS logs

## Create Reusable Objects

### Layer 2 Based Testing

1. `Performance Testing > Objects > Networks`
2. Create a new named object
3. On the __Client__ section:
    * Identify which NIC you want FTS to generate outbound traffic towards the DUT
    * Specify the network range that the FTS Client port will be participating in
    * Specify the peer network range that you expect to receive return traffic from (should mirror the __Server__ side network)
    * Make sure to remove any additional network subnets that may be defined
4. On the __Server__ section:
    * Identify which NIC you want FTS to expect inbound traffic from the DUT
    * Specify the network range that the FTS Server port will be participating in
    * Specify the peer network range that you expect to receive return traffic from (should mirror the __Client__ side network)
    * Make sure to remove any additional network subnets that may be defined

#### Example

![Network Object](./fts_network_object.png "Example Network Object")

### Layer 3 Based Testing

1. `Performance Testing > Objects > Networks`
2. Create a new named object
3. On the __Client__ section:
    * Identify which NIC you want FTS to generate outbound traffic towards the DUT
    * Specify the network range that the FTS Client port will be participating in
    * Specify the peer network range that you expect to receive return traffic from (should mirror the __Server__ side network)
    * Make sure to remove any additional network subnets that may be defined
4. On the __Server__ section:
    * Identify which NIC you want FTS to expect inbound traffic from the DUT
    * Specify the network range that the FTS Server port will be participating in
    * Specify the peer network range that you expect to receive return traffic from (should mirror the __Client__ side network)
    * Make sure to remove any additional network subnets that may be defined

#### Example

![Network Object](./fts_network_object.png "Example Network Object")

## Testing Layer 2 Switching Speeds (Frames)

1. 

## Testing Layer 3 Routing/Firewall Speeds (Packets)

