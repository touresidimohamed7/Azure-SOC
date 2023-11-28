![Building a SOC + Honeynet in Azure Live Traffic (2)](https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/d46a545f-48aa-4803-afe8-7a0a6588eaca)

## Introduction

In this project, I construct a miniature honeynet on Azure, aggregating logs from diverse sources into a Log Analytics workspace. Microsoft Sentinel utilizes this data to generate attack maps, trigger alerts, and establish incidents. After assessing security metrics in an insecure environment for 24 hours, I implement security controls to fortify the setup, measure metrics for an additional 24 hours, and present the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![2](https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/6ea88b84-06ec-4a7e-9c27-dd726c041ad8)



## Architecture After Hardening / Security Controls
![3](https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/4ec29d01-0eb9-43d0-83db-a067dd711b02)


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
<img width="1390" alt="nsg-malicious" src="https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/7a26d394-bd9e-4703-8fbd-5d6c20bc0892">
<img width="1388" alt="syslog-ssh-auth-fail" src="https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/5de866bf-6eef-45fa-841b-8750dd8e3761">
<img width="1374" alt="windows-rdp-auth-fail" src="https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/e417ba13-8227-40a1-bea9-d65999c3fc6e">
<img width="1372" alt="mssql-auth-fail" src="https://github.com/touresidimohamed7/Azure-SOC/assets/152078244/764e9910-72c9-4fcd-9596-887f685b7de1">

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-09-17 11:03:27
Stop Time 2023-09-18 17:03:27



| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 18360
| Syslog                   | 3017
| SecurityAlert            | 12
| SecurityIncident         | 337
| AzureNetworkAnalytics_CL | 732

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-09-20 13:07
Stop Time	2023-09-21 13:07

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 76667
| Syslog                   | 29
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a miniature honeynet was established in Microsoft Azure, integrating log sources into a Log Analytics workspace. Microsoft Sentinel played a pivotal role in generating alerts and incidents based on the ingested logs. Furthermore, metrics were assessed in the insecure environment both before and after the application of security controls. Notably, the implementation of these controls led to a significant reduction in the number of security events and incidents, showcasing their efficacy.

It's important to acknowledge that if the network resources were heavily utilized by regular users, there might have been a potential increase in security events and alerts within the 24-hour period following the implementation of the security controls.
