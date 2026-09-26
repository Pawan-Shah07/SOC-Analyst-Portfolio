# VMware Workstation 17 Pro Installation

## Overview

VMware Workstation 17 Pro is used as the virtualization platform for the Virtual SOC Home Lab. It provides the isolated virtual environment required to deploy the firewall, attacker machine, monitored endpoint, and SIEM infrastructure.

## Software

* **Virtualization Platform:** VMware Workstation 17 Pro
* **Host Operating System:** Windows
* **Purpose:** Host and manage the Virtual SOC laboratory environment

## Installation Process

### 1. Obtain VMware Workstation

The VMware Workstation 17 Pro installer is obtained from the official VMware/Broadcom software distribution platform.

### 2. Start the Installer

The VMware Workstation installer is launched with administrator privileges.

The installation wizard is followed to begin the installation process.

### 3. Accept the License Agreement

The VMware license agreement is reviewed and accepted to continue the installation.

### 4. Select Installation Location

The default installation location is retained unless a different location is required.

### 5. Configure Installation Options

The available installation options are reviewed and the required options are selected.

### 6. Complete the Installation

The installation is completed using the VMware Workstation installation wizard.

After installation finishes, VMware Workstation is launched to verify that the application is functioning correctly.

## Verification

The installation is verified by:

* Launching VMware Workstation 17 Pro.
* Creating and managing virtual machines.
* Accessing the Virtual Network Editor.
* Confirming that the required virtual networking features are available.

## Virtual Networking

Two VMware virtual networks are used for the SOC lab.

| Virtual Network | Type      | Purpose                | Network           |
| --------------- | --------- | ---------------------- | ----------------- |
| `vmnet8`        | NAT       | WAN / external network | `172.16.10.0/24`  |
| `vmnet2`        | Host-only | Internal SOC LAN       | `192.168.10.0/24` |

The virtual networks provide separation between the simulated external attacker network and the internal SOC network.

### WAN Network

`vmnet8` provides the WAN-side connectivity used by the Kali Linux attacker machine and the WAN interface of pfSense.

### LAN Network

`vmnet2` provides the isolated internal network used by the Windows endpoint and Ubuntu Wazuh server.

## Role in the SOC Lab

VMware Workstation provides the virtualization layer for the entire security laboratory.

The virtual environment allows the following systems to operate together:

```text
VMware Workstation
        │
        ├── Kali Linux
        │
        ├── pfSense
        │
        ├── Windows 10
        │
        └── Ubuntu Server
                │
                └── Wazuh Manager
```

This isolated environment allows security events and controlled attack scenarios to be generated without requiring separate physical systems.

## Installation Evidence

Screenshots were not captured during the original VMware Workstation installation. Therefore, this document focuses on the installation procedure and the resulting configuration rather than presenting recreated installation screenshots.

The current VMware installation and virtual networking configuration are verified through the functioning SOC laboratory environment.
