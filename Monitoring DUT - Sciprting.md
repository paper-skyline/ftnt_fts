# Monitoring DUT & Pre/Post Test Scripting

## Configure a DUT Object SNMP Monitor

_During a test, FortiTester can monitor the DUT via SNMP, which gets sourced from the FTS Management Port. __Remember to configure the DUT to accept SNMP from the FTS.___

1. `Security/Performance Testing -> Objects -> SNMP Monitors`
2. Create a new named object for the DUT
3. Specify the DUT's Management IP and SNMP Community Name
4. Specify which specific DUT SNMP OID's that you want to monitor

### Monitoring the DUT During Testing Example



## Config a Script to Clear FortiGate Sessions

1. `Security/Performance Testing -> Objects -> Scripts`
2. Create a new named script
3. Specify the Username, Password, and DUT Management IP address
4. Define the Pre-Test and/or Post-Test Parameters
    * API endpoint details can be found on [Fortinet's Developer Network (FNDN) site](https://fndn.fortinet.net)
    * POST /api/v2/monitor/firewall/session/clear_all/  # FOSv7.0.x specific
    * POST /api/v2/monitor/firewall/session/close-all/  # FOSv7.2.x specific