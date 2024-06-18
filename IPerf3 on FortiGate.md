# IPerf3 Testing on a FortiGate

On a _somewhat_ related note, FortiGate devices are capable of performing basic iperf3 tests from the CLI. Here's two brief use cases and some related documentation for further reading. Fortinet sells an automated service that automatically measures and updates both upload and download bandwidth fields for WAN ports called "FortiGuard SD-WAN Underlay Bandwidth and Quality Monitoring Service" that _I suspect_ leverages this tool at least in some part.

## Use Cases

There are several different options that can be used with iperf on the FortiGate through the CLI. In addition to basic TCP and UDP thruput testing, you can launch parallel tests, reverse tests, rate limited tests, and a few more.

1. Perform Loopback Testing Between Two Ports on a FortiGate

```ruby
diag traffictest server-intf <port> # Define a port on the FortiGate to use
diag traffictest client-intf <port> # Define a port on the FortiGate to use
diag traffictest run                # Launch the IPerf3 test
```

2. TCP/UDP Traffic Test Against an IPerf Server

```ruby
diag traffictest server-intf <port> # Define a port on the FortiGate to use. _In this scenario, both server and client port should be the same._
diag traffictest client-intf <port> # Define a port on the FortiGate to use _In this scenario, both server and client port should be the same._
diag traffictest port <port>        # Default port is tcp/5209 but will vary from server to server
diag traffictest run -c <ipv4>      # Launch a TCP IPerf3 test
```

_alternatively_ you can run a __UDP__ test

```ruby
diag traffictest server-intf <port> # Define a port on the FortiGate to use. _In this scenario, both server and client port should be the same._
diag traffictest client-intf <port> # Define a port on the FortiGate to use _In this scenario, both server and client port should be the same._
diag traffictest port <port>        # Default port is tcp/5209 but will vary from server to server
diag traffictest run -c -u <ipv4>   # Launch a TCP IPerf3 test
```

3. Run Several TCP Traffic Tests in Parallel

```ruby
diag traffictest server-intf <port> # Define a port on the FortiGate to use. _In this scenario, both server and client port should be the same._
diag traffictest client-intf <port> # Define a port on the FortiGate to use _In this scenario, both server and client port should be the same._
diag traffictest port <port>        # Default port is tcp/5209 but will vary from server to server
diag traffictest run -c <ipv4> -P 5 # Launch 5 TCP IPerf3 tests in parallel
```

### Example

```ruby
splatter # diag traffictest server-intf wan1
server-intf:    wan1

splatter # diag traffictest client-intf wan1
client-intf:    wan1

splatter # diag traffictest port 5209
port:   5209

splatter # diag traffictest run -c 23.19.208.9 -P 5
Connecting to host 23.19.208.9, port 5209
[  6] local 174.171.5.29 port 9513 connected to 23.19.208.9 port 5209
[  8] local 174.171.5.29 port 9514 connected to 23.19.208.9 port 5209
[ 10] local 174.171.5.29 port 9515 connected to 23.19.208.9 port 5209
[ 12] local 174.171.5.29 port 9516 connected to 23.19.208.9 port 5209
[ 14] local 174.171.5.29 port 9517 connected to 23.19.208.9 port 5209
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  6]   0.00-1.00   sec   720 KBytes  5.89 Mbits/sec    0   59.4 KBytes
[  8]   0.00-1.00   sec   757 KBytes  6.19 Mbits/sec    0   60.8 KBytes
[ 10]   0.00-1.00   sec   748 KBytes  6.12 Mbits/sec    0   59.4 KBytes
[ 12]   0.00-1.00   sec   819 KBytes  6.70 Mbits/sec    0   66.5 KBytes
[ 14]   0.00-1.00   sec  1.39 MBytes  11.7 Mbits/sec    0    143 KBytes
[SUM]   0.00-1.00   sec  4.36 MBytes  36.6 Mbits/sec    0
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   1.00-2.00   sec   850 KBytes  6.97 Mbits/sec    0   84.8 KBytes
[  8]   1.00-2.00   sec   865 KBytes  7.09 Mbits/sec    0   87.7 KBytes
[ 10]   1.00-2.00   sec   834 KBytes  6.84 Mbits/sec    0   86.3 KBytes
[ 12]   1.00-2.00   sec   911 KBytes  7.46 Mbits/sec    0   96.2 KBytes
[ 14]   1.00-2.00   sec  1.69 MBytes  14.2 Mbits/sec    0    192 KBytes
[SUM]   1.00-2.00   sec  5.07 MBytes  42.5 Mbits/sec    0
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   2.00-3.01   sec   792 KBytes  6.45 Mbits/sec    0    107 KBytes
[  8]   2.00-3.01   sec   881 KBytes  7.17 Mbits/sec    0    115 KBytes
[ 10]   2.00-3.01   sec   872 KBytes  7.10 Mbits/sec    0    112 KBytes
[ 12]   2.00-3.01   sec   932 KBytes  7.59 Mbits/sec    0    120 KBytes
[ 14]   2.00-3.01   sec  1.74 MBytes  14.5 Mbits/sec    0    238 KBytes
[SUM]   2.00-3.01   sec  5.14 MBytes  42.8 Mbits/sec    0
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   3.01-4.01   sec  1.03 MBytes  8.64 Mbits/sec    3   39.6 KBytes
[  8]   3.01-4.01   sec   981 KBytes  8.03 Mbits/sec    5   45.2 KBytes
[ 10]   3.01-4.01   sec  1.11 MBytes  9.30 Mbits/sec    7   59.4 KBytes
[ 12]   3.01-4.01   sec  1.15 MBytes  9.66 Mbits/sec    5   62.2 KBytes
[ 14]   3.01-4.01   sec   888 KBytes  7.27 Mbits/sec    3   25.5 KBytes
[SUM]   3.01-4.01   sec  5.12 MBytes  42.9 Mbits/sec   23
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   4.01-5.01   sec  1.23 MBytes  10.3 Mbits/sec    0   62.2 KBytes
[  8]   4.01-5.01   sec   940 KBytes  7.69 Mbits/sec    0   45.2 KBytes
[ 10]   4.01-5.01   sec  1020 KBytes  8.34 Mbits/sec    1   49.5 KBytes
[ 12]   4.01-5.01   sec  1.27 MBytes  10.6 Mbits/sec    1   60.8 KBytes
[ 14]   4.01-5.01   sec   592 KBytes  4.84 Mbits/sec    0   29.7 KBytes
[SUM]   4.01-5.01   sec  4.99 MBytes  41.8 Mbits/sec    2
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   5.01-6.01   sec  1.15 MBytes  9.66 Mbits/sec    1   50.9 KBytes
[  8]   5.01-6.01   sec   994 KBytes  8.14 Mbits/sec    0   48.1 KBytes
[ 10]   5.01-6.01   sec  1.05 MBytes  8.82 Mbits/sec    0   52.3 KBytes
[ 12]   5.01-6.01   sec  1.30 MBytes  10.9 Mbits/sec    0   63.6 KBytes
[ 14]   5.01-6.01   sec   495 KBytes  4.05 Mbits/sec    1   28.3 KBytes
[SUM]   5.01-6.01   sec  4.96 MBytes  41.6 Mbits/sec    2
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   6.01-7.02   sec  1.14 MBytes  9.43 Mbits/sec    0   60.8 KBytes
[  8]   6.01-7.02   sec  1024 KBytes  8.30 Mbits/sec    1   38.2 KBytes
[ 10]   6.01-7.02   sec  1.17 MBytes  9.69 Mbits/sec    0   59.4 KBytes
[ 12]   6.01-7.02   sec  1.10 MBytes  9.18 Mbits/sec    1   58.0 KBytes
[ 14]   6.01-7.02   sec   597 KBytes  4.84 Mbits/sec    0   32.5 KBytes
[SUM]   6.01-7.02   sec  4.99 MBytes  41.4 Mbits/sec    2
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   7.02-8.00   sec  1.19 MBytes  10.1 Mbits/sec    0   63.6 KBytes
[  8]   7.02-8.00   sec   871 KBytes  7.24 Mbits/sec    0   50.9 KBytes
[ 10]   7.02-8.00   sec  1024 KBytes  8.51 Mbits/sec    2   35.4 KBytes
[ 12]   7.02-8.00   sec  1.19 MBytes  10.2 Mbits/sec    0   63.6 KBytes
[ 14]   7.02-8.00   sec   694 KBytes  5.77 Mbits/sec    0   38.2 KBytes
[SUM]   7.02-8.00   sec  4.91 MBytes  41.8 Mbits/sec    2
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   8.00-9.01   sec  1.11 MBytes  9.30 Mbits/sec    1   56.6 KBytes
[  8]   8.00-9.01   sec  1.17 MBytes  9.77 Mbits/sec    0   55.1 KBytes
[ 10]   8.00-9.01   sec   755 KBytes  6.17 Mbits/sec    1   32.5 KBytes
[ 12]   8.00-9.01   sec  1.21 MBytes  10.1 Mbits/sec    1   58.0 KBytes
[ 14]   8.00-9.01   sec   800 KBytes  6.54 Mbits/sec    0   43.8 KBytes
[SUM]   8.00-9.01   sec  5.01 MBytes  41.9 Mbits/sec    3
- - - - - - - - - - - - - - - - - - - - - - - - -
[  6]   9.01-10.01  sec  1.13 MBytes  9.45 Mbits/sec    0   63.6 KBytes
[  8]   9.01-10.01  sec  1.01 MBytes  8.45 Mbits/sec    0   56.6 KBytes
[ 10]   9.01-10.01  sec   731 KBytes  5.96 Mbits/sec    0   38.2 KBytes
[ 12]   9.01-10.01  sec  1.18 MBytes  9.84 Mbits/sec    0   63.6 KBytes
[ 14]   9.01-10.01  sec   984 KBytes  8.02 Mbits/sec    0   50.9 KBytes
[SUM]   9.01-10.01  sec  5.00 MBytes  41.7 Mbits/sec    0
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  6]   0.00-10.01  sec  10.3 MBytes  8.62 Mbits/sec    5             sender
[  6]   0.00-10.07  sec  10.2 MBytes  8.49 Mbits/sec                  receiver
[  8]   0.00-10.01  sec  9.32 MBytes  7.81 Mbits/sec    6             sender
[  8]   0.00-10.07  sec  9.27 MBytes  7.72 Mbits/sec                  receiver
[ 10]   0.00-10.01  sec  9.17 MBytes  7.68 Mbits/sec   11             sender
[ 10]   0.00-10.07  sec  9.07 MBytes  7.56 Mbits/sec                  receiver
[ 12]   0.00-10.01  sec  11.0 MBytes  9.22 Mbits/sec    8             sender
[ 12]   0.00-10.07  sec  10.9 MBytes  9.12 Mbits/sec                  receiver
[ 14]   0.00-10.01  sec  9.75 MBytes  8.17 Mbits/sec    4             sender
[ 14]   0.00-10.07  sec  9.52 MBytes  7.93 Mbits/sec                  receiver
[SUM]   0.00-10.01  sec  49.5 MBytes  41.5 Mbits/sec   34             sender
[SUM]   0.00-10.07  sec  49.0 MBytes  40.8 Mbits/sec                  receiver

iperf Done.
```

## Documentation

* [Fortinet Community Article with Examples](https://community.fortinet.com/t5/FortiGate/Technical-Tip-Use-cases-for-the-diagnose-traffictest-command/ta-p/197784?externalID=FD45599)
* [List of Public IPerf Servers](https://github.com/R0GGER/public-iperf3-servers)
* [IPerf Official Site](https://iperf.fr/)