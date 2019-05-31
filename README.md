# Paloalto_SNMPv3_zabbix4.0
Template for monitoring Palo alto firewall PAN OS 8.1 for zabbix 4.0

# Features
- CPU discovery
- Fan discovery
- Temperature discovery
- Storage discovery
- Interface discovery
- Traps for restart and HA failuire

# Tested
 - zabbix 4.0 (CentOS 7)
 - PANOS 8.1
 
 # Configuration
1. cofigure palo alto SNMPv3 use this guide: https://knowledgebase.paloaltonetworks.com/KCSArticleDetail?id=kA10g000000ClG6CAK
 - If you have HA configured in step 2. of this guide when polling the engineID you need to poll it for both servers because it differs.
2. download and add MIB files for palo alto from official site: https://docs.paloaltonetworks.com/resources/snmp-mib-files
3. configure zabbix snmptraps support if you haven't done so allready: https://www.zabbix.com/documentation/4.0/manual/config/items/itemtypes/snmptrap 
4. add theese lines in /etc/snmptt.conf file:
```
EVENT general panGeneralSystemShutdownTrap "System shutdown" Critical
FORMAT ZBXTRAP $ar $Fn $8 - eventID: $9 - $13

EVENT general panGeneralGeneralTrap "General trap" Normal
FORMAT ZBXTRAP $ar $Fn $8 - eventID: $9 - $13

EVENT general panHAHa2LinkChangeTrap "HA link change" Critical
FORMAT ZBXTRAP $ar $Fn $8 - eventID: $9 - $13

EVENT general panHASessionSynchTrap "HA session synchronization" Critical
FORMAT ZBXTRAP $ar $Fn $8 - eventID: $9 - $13

EVENT general panHAConnectChangeTrap "HA connection" Critical
FORMAT ZBXTRAP $ar $Fn $8 - eventID: $9 - $13

EVENT general .* "General event" Normal
FORMAT ZBXTRAP $ar $Fn $+*
```
