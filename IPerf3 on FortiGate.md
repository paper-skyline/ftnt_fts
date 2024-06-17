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

## Documentation

[Fortinet Community Article with Examples](https://community.fortinet.com/t5/FortiGate/Technical-Tip-Use-cases-for-the-diagnose-traffictest-command/ta-p/197784?externalID=FD45599)
[List of Public IPerf Servers](https://github.com/R0GGER/public-iperf3-servers)
[IPerf Official Site](https://iperf.fr/)