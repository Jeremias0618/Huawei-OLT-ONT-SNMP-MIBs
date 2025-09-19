# Huawei OLT/ONT SNMP MIBs

This repository contains a comprehensive collection of SNMP MIBs and OIDs for monitoring and managing Huawei OLTs and ONTs.

The OIDs in this collection are primarily from **Huawei SmartAX MA5600T/MA5603T/MA5608T OLTs**, but they should work on other Huawei OLT models as well.

⚠️ **Disclaimer:**  
These OIDs are shared for reference. They have not been fully tested in all environments. If you successfully use them in production, please share your experience or improvements.

## Table of Contents

- [Example Usage](#example-usage)
- [Common Huawei OLT/ONT OIDs](#common-huawei-oltont-oids)
  - [ONU Information](#onu-information)
  - [OLT and Slot Information](#olt-and-slot-information)
  - [Interfaces](#interfaces)
  - [ONT Traffic Statistics](#ont-traffic-statistics)
  - [GPON and VLAN Status](#gpon-and-vlan-status)
  - [System Info](#system-info)
  - [ONU Disconnection Reasons](#onu-disconnection-reasons)
- [Additional Useful OIDs](#additional-useful-oids)
- [RX Power OIDs](#rx-power-oids)
- [Huawei Specific OIDs](#huawei-specific-oids)
- [Contributions](#contributions)

---

## Example Usage

Basic SNMP command syntax for Linux:

```bash
snmpwalk -v <version> -c <community> <ip_olt> <oid>
```

**Examples:**

```bash
# Get interface descriptions
snmpwalk -v 2c -c public 192.168.1.10 1.3.6.1.2.1.2.2.1.2

# Check ONU status
snmpwalk -v 2c -c public 192.168.1.10 1.3.6.1.4.1.2011.6.128.1.1.2.62.1.22

# Get board temperature
snmpwalk -v 2c -c public 192.168.1.10 1.3.6.1.4.1.2011.2.6.7.1.1.2.1.10

# Get OLT uptime
snmpwalk -v 2c -c public 192.168.1.10 1.3.6.1.2.1.1.3
```

**Alternative SNMP tools:**
- SNMPwalk (Windows/Linux)
- SNMP Browser applications
- Network monitoring tools (Zabbix, Nagios, etc.)

---

## Common Huawei OLT/ONT OIDs

### ONU Information

* **ONT description**
  `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.9`
* **ONT MAC/Serial number**
  `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.3`
* **Line profile name**
  `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.7`
* **ONT service profile name**
  `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.8`
* **Optical power of the ONU (RX)**
  `1.3.6.1.4.1.2011.6.128.1.1.2.51.1.4`
* **ONU status (1 = Online, 2 = Offline)**
  `1.3.6.1.4.1.2011.6.128.1.1.2.62.1.22` (hwGponDeviceOntEthernetOnlineState)
* **Alternative ONU status OID**
  `1.3.6.1.4.1.2011.6.128.1.1.2.46.1.15`
* **ONU optical temperature**
  `1.3.6.1.4.1.2011.6.128.1.1.2.51.1.1` (hwGponOntOpticalDdmTemperature)
* **Number of MAC addresses connected to ONU**
  `1.3.6.1.4.1.2011.6.128.1.1.2.46.1.21` (hwGponDeviceOntControlMacCount)
* **Distance to the ONU**
  `1.3.6.1.4.1.2011.6.128.1.1.2.46.1.20` (hwGponDeviceOntControlRanging)
* **Last ONU disconnection reason**
  `1.3.6.1.4.1.2011.6.128.1.1.2.46.1.24`

---

### OLT and Slot Information

* **Board temperature**
  `1.3.6.1.4.1.2011.2.6.7.1.1.2.1.10` (hwMusaBoardTemperature)
* **Slot temperature**
  `1.3.6.1.4.1.2011.6.3.3.2.1.13` (hwSlotTemprature)
* **Processor board load (CPU rate)**
  `1.3.6.1.4.1.2011.2.6.7.1.1.2.1.5` (hwMusaBoardCpuRate)
* **Frame power status**
  `1.3.6.1.4.1.2011.2.6.7.1.1.1.1.11` (hwMusaFramePower)
* **Slot table**
  `1.3.6.1.4.1.2011.6.3.3.2` (hwSlotTable)

---

### Interfaces

* **Interface description**
  `1.3.6.1.2.1.2.2.1.2`
* **Traffic counters**

  * Inbound: `1.3.6.1.2.1.2.2.1.10`
  * Outbound: `1.3.6.1.2.1.2.2.1.16`

---

### ONT Traffic Statistics

* **ONT inbound bytes**
  `1.3.6.1.4.1.2011.6.128.1.1.4.23.1.4`
* **ONT outbound bytes**
  `1.3.6.1.4.1.2011.6.128.1.1.4.23.1.3`

---

### GPON and VLAN Status

* **GPON port link status (1 = Online, 2 = Offline)**
  `1.3.6.1.4.1.2011.6.128.1.1.2.21.1.10` (hwGponDeviceOltControlStatus)
* **VLAN interface status (up/down)**
  `1.3.6.1.4.1.2011.5.6.1.2.1.5` (hwVlanInterfaceAdminStatus)

---

### System Info

* **OLT uptime**
  `1.3.6.1.2.1.1.3`
* **SNMP packet counters**

  * Inbound: `1.3.6.1.2.1.11.1`
  * Outbound: `1.3.6.1.2.1.11.2`

---

### ONU Disconnection Reasons

The following OID provides the reason for the last disconnection of an ONU:
* **Last ONU disconnection reason**
  `1.3.6.1.4.1.2011.6.128.1.1.2.46.1.24`

**Disconnection reason codes:**

| Code | Reason |
|------|--------|
| 1 | LOS (Loss of signal) |
| 2 | LOSi (Loss of signal for ONUi) or LOBi (Loss of burst for ONUi) |
| 3 | LOFI (Loss of frame of ONUi) |
| 4 | SFI (Signal fail of ONUi) |
| 5 | LOAI (Loss of acknowledge with ONUi) |
| 6 | LOAMI (Loss of PLOAM for ONUi) |
| 7 | Deactive ONT fails |
| 8 | Deactive ONT success |
| 9 | Reset ONT |
| 10 | Re-register ONT |
| 11 | Pop up fail |
| 13 | Dying-gasp |
| 15 | LOKI (Loss of key synch with ONUi) |
| 18 | Deactivated ONT due to the ring |
| 30 | Shut down ONT optical module |
| 31 | Reset ONT by ONT command |
| 32 | Reset ONT by ONT reset button |
| 33 | Reset ONT by ONT software |
| 34 | Deactivated ONT due to broadcast attack |
| 35 | Operator check fail |
| 37 | Rogue ONT detected by itself |
| -1 | Query fails |

---

## Additional Useful OIDs

* `1.3.6.1.4.1.2011.5.14.1.4.1.6` → hwMaxMacLearn
* `1.3.6.1.4.1.2011.5.14.1.3` → hwMacExpire
* `1.3.6.1.4.1.2011.5.14.6.1.1.15` → hwOpticsMDWaveLength
* `1.3.6.1.4.1.2011.5.14.6.1.1.11` → hwOpticsMDVendorName
* `1.3.6.1.4.1.2011.5.21.1.7` → hwRingCheckAdminStatus
* `1.3.6.1.4.1.2011.5.6.1.2.1.1` → hwVlanInterfaceID
* `1.3.6.1.4.1.2011.5.6.1.2` → hwVlanInterfaceTable
* `1.3.6.1.4.1.2011.5.6.1.1.1.2` → hwVlanName
* `1.3.6.1.2.1.5.8` → icmpInEchos
* `1.3.6.1.2.1.4.20.1` → ipAddrEntry

---

## RX Power OIDs

* **OLT RX:**
  `SNMPv2-SMI::enterprises.2011.6.128.1.1.2.51.1.6`
* **ONU RX:**
  `SNMPv2-SMI::enterprises.2011.6.128.1.1.2.51.1.4`

---

## Huawei Specific OIDs

### Unconfigured ONU

* `1.3.6.1.4.1.2011.6.128.1.1.2.52.1.2`

### Confirmed ONU

* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.2.{PortID}.4294967295` → Status = `1`
* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.3.{PortID}.4294967295` → SN = `5a544547c1b2f8fc`
* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.7.{PortID}.4294967295` → Line Profile = `"Drinia"`
* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.8.{PortID}.4294967295` → Service Profile = `"HG8247H"`
* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.6.{PortID}.4294967295` → `1`
* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.10.{PortID}.4294967295` → `1`

### WAN Profiles

**DHCP**

* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.1.{PortID}.0.0` → `1` (DHCP)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.8.{PortID}.0.0` → VLAN = `20`
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.9.{PortID}.0.0` → Priority = `0`

**Static**

* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.1.{PortID}.0.0` → `2` (Static)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.2.{PortID}.0.0` → `172.16.0.2` (IP Address)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.3.{PortID}.0.0` → `255.255.240.0` (Subnet Mask)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.5.{PortID}.0.0` → `172.16.0.1` (Default GW)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.6.{PortID}.0.0` → `172.16.0.1` (Default GW)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.7.{PortID}.0.0` → `8.8.8.8` (DNS)
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.8.{PortID}.0.0` → VLAN = `100`
* `.1.3.6.1.4.1.2011.6.128.1.1.2.49.1.9.{PortID}.0.0` → `0`

### TR-069

* `1.3.6.1.4.1.2011.6.145.1.1.1.13.1.3.{PortID}.3` → TR069 = `"Drinia"`

### Service Port

* `.1.3.6.1.4.1.2011.5.14.5.2.1.2.4294967295` → Shelf = `0`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.3.4294967295` → Slot = `0`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.4.4294967295` → Port = `0`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.5.4294967295` → ONU ID = `1`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.6.4294967295` → Gemport = `1`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.7.4294967295` → Multiservice = `4`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.8.4294967295` → VLAN = `20`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.9.4294967295` → Inbound = `9`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.10.4294967295` → Outbound = `9`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.11.4294967295` → `1`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.12.4294967295` → VLAN = `20`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.18.4294967295` → `2`
* `.1.3.6.1.4.1.2011.5.14.5.2.1.15.4294967295` → `1` (DELETE 6)

### Delete ONU/ServicePort

* `.1.3.6.1.4.1.2011.5.14.5.2.1.15.{SERVICEPORTID}` → `6` (Delete ServicePort)
* `1.3.6.1.4.1.2011.6.128.1.1.2.43.1.10.{PortID}.1` → `6` (Delete ONU)

---

## Contributions

If you have validated OIDs, tested configurations, or additional Huawei SNMP MIBs, feel free to open a pull request or share them in the issues section.
