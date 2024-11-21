# Building a Cloud SOC in Azure + Honeynet
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I designed and deployed a mini honeynet in Azure, configuring it to ingest log data from various resources into a Log Analytics workspace. Microsoft Sentinel was then utilized to create attack maps, trigger alerts, and manage incidents. Over a 24-hour period, I measured key security metrics in the initial, unsecured environment. After implementing security controls to harden the setup, I collected metrics for an additional 24 hours. The results of this comparison are detailed below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![before nsg](https://github.com/user-attachments/assets/525c7e78-0aee-4bca-97f4-333b19620540)

![linux before](https://github.com/user-attachments/assets/d428ecc3-3da8-49fe-9061-30f3dbd4b5fc)

![Windows before](https://github.com/user-attachments/assets/1b266a96-0938-4ece-bbf2-5a9d927904d8)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
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

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
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

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
