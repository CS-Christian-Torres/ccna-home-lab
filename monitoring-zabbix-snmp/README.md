# SNMP Monitoring with Zabbix

Extended the lab by adding centralized monitoring via SNMP and Zabbix, 
running on a Raspberry Pi on the management VLAN (192.168.10.0/24).

## What was done
- Enabled SNMP (v2c, read-only) on R1, R2, R3, SW1, SW2
- Advertised the management network into OSPF Area 0 so devices 
  behind R1 (R2, R3) were reachable from the Pi
- Added all 5 devices as hosts in Zabbix using the built-in 
  "Cisco IOS by SNMP" template
- Validated monitoring by simulating a link failure (disconnected SW1) 
  and confirming Zabbix detected the outage and later marked it resolved

## Key finding
Disconnecting SW1 also broke SNMP reachability to R1, R2, R3, and SW2, 
since their management traffic depended on that link. This highlighted 
a single point of failure in the topology worth addressing with 
redundant links or a separate out-of-band management path.

## Config
See [configs/snmp-config.txt](configs/snmp-config.txt)
