# Building a Cloud SOC in Azure + Honeynet
![Cloud SOC Honeynet](https://github.com/user-attachments/assets/eee186a7-f7b1-48a0-9362-7949d2e52b66)


## Introduction

In this project, I designed and deployed a mini honeynet in Azure, configuring it to ingest log data from various resources into a Log Analytics workspace. Microsoft Sentinel was then utilized to create attack maps, trigger alerts, and manage incidents. Over a 24-hour period, I measured key security metrics in the initial, unsecured environment. After implementing security controls to harden the setup, I collected metrics for an additional 24 hours. The results of this comparison are detailed below. The security metrics used are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls disabled, and all other resources were deployed with public endpoints visible to the Internet.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my personal workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint.

## Attack Maps Before Hardening / Security Controls
![before nsg](https://github.com/user-attachments/assets/525c7e78-0aee-4bca-97f4-333b19620540)

![linux before](https://github.com/user-attachments/assets/d428ecc3-3da8-49fe-9061-30f3dbd4b5fc)

![Windows before](https://github.com/user-attachments/assets/1b266a96-0938-4ece-bbf2-5a9d927904d8)


## Metrics Before Hardening / Security Controls

The following table shows the metrics I measured in my insecure environment for the initial 24 hours:
Start Time 2024-11-17 01:23:31
Stop Time 2024-11-18 01:23:31

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 216804
| Syslog                   | 4056
| SecurityAlert            | 0
| SecurityIncident         | 257
| AzureNetworkAnalytics_CL | 4816

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24-hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics I measured in my environment for another 24 hours, but after I implemented security controls:
Start Time 2024-11-19 18:22:34
Stop Time	2024-11-20 18:22:34

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 811
| Syslog                   | 2
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, I built a mini honeynet in Microsoft Azure and integrated log sources into a Log Analytics workspace. Using Microsoft Sentinel, I set up alerts and incident tracking based on the collected logs. I measured security metrics in the initial, unsecured environment, then applied security controls to harden it and measured the metrics again. The results showed a significant drop in security events and incidents after implementing the controls, highlighting their effectiveness.
