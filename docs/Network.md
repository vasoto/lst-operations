I have slightly modified the VLAN assignment of the TCS servers
and introduced policy based routing to enable all possible combinations between the servers.
VLAN 10 and 50 are not affected, only those which are routed through the main nexus switch are affected. Here is the summary of the current status

  
TCS01:  VLAN100 10.200.100.101; VLAN1001 10.1.4.1
TCS02:  VLAN100 10.200.100.102; VLAN1008  10.1.8.1; VLAN1010 10.1.10.20
TCS03 (unbonded!): VLAN100 10.200.100.103; VLAN100 10.200.100.93
TCS04 (unbonded!): VLAN100 10.200.100.104; VLAN100 10.200.100.94
TCS05: VLAN100 10.200.100.105; VLAN1011 10.1.11.2
TCS06: VLAN100 10.200.100.106
TCS07: VLAN100 10.200.100.107; VLAN1007 10.1.7.250

Virtual machines:
TCS02: 10.1.8.3 VLAN1008
TCS05: 10.200.100.80 VLAN100
(anything missing?)

Pending:
- bond interfaces on TCS03 and TCS04. Dirk and Julien, please plan to test that. 
- X-check Osaka, configure Okinawa (I wait for Taka to be back in the institute)

With this configuration:
- tcs01 provides IPs through dhcp to the WR switch, UCTS and TIB (also should do that for the GPS but it is down)
- CDTS can be run on tcs07 (please check)
- all servers can be accessed from everywhere once you are on a machine connected to the nexus switch (including the 6 servers in the commissioning container). Reminder: their IPs are 10.204.80.1-6 (VLAN80)

Let me know if there are questions / comments