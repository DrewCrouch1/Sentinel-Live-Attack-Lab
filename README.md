# Microsoft Azure/Sentinel Honeypot

## Description:
This GitHub repository hosts a project that sets up a mini honeypot using Microsoft Azure and Sentinel, designed to capture and analyze failed Remote Desktop Protocol (RDP) login attempts. The project utilizes Azure infrastructure, Log Analytics Workspace, and Sentinel for log collection, analysis, and visualization.

## Key Features:

### Honeypot Configuration:

A Windows 10 Virtual Machine is created on Microsoft Azure.
The Network Security Group (NIC NSG) is configured to allow all inbound traffic for any destination port or protocol on the virtual machine.

![LA1](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/051967e2-443a-41dc-9b27-ba4f60c694e3)

![LA2](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/c0b86fb6-c0b2-49ac-a312-b64622a62795)


### Log Collection and Analysis:

A Log Analytics Workspace is created to collect data from the Azure virtual machine.
Sentinel is set up and connected to the Log Analytics Workspace for advanced threat detection and analysis.

### Failed Login Tracking:

The VM's firewall is deliberately taken down to allow outside connections.
Event ID 4625 is monitored to track failed RDP login attempts.

![LA3](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/ab9c7eef-a75a-4a8a-b30c-6724221b2334)

![LA4](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/67a6ec45-c4d9-4b0f-85c6-7b0f3e69f1a7)


### Location Data Extraction:

A PowerShell script is executed to extract Security events with Event ID 4625.
The script utilizes the ipgeolocation.io API to transform IP addresses into detailed location data (country, city, state, province, local currency, latitude, longitude, company details, ISP lookup, language, and zip code).

![LA5](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/bdd35b85-7019-449d-920f-874b3b9f7689)

![LA6](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/aa78f294-e7e5-4079-9a90-74962cdcbdbf)


### Custom Log Creation:

The PowerShell script appends the extracted data to a custom log file (failed_rdp.log).

![LA7](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/26c15881-5008-432e-87e8-7a28d5222bf1)


### Sentinel Integration:

A custom log in Azure is created to capture the failed_rdp.log file and bring it into Sentinel.
Log Analytics Workspace is used to import and store the custom log data.

![LA8](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/dde69d37-1d33-48ce-8a6d-71035736379f)

![LA9](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/dc5864a0-d7f4-4894-a725-f54bf91adc1c)

### Visualization:

A KQL (Kusto Query Language) query is crafted to separate raw data into columns for use within Sentinel.
The query is executed with a visualization that creates a heat map of failed RDP attempts by location.

![LA11](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/e630c8ed-4db6-4e23-b785-8c571f1f1cc6)

![LA12](https://github.com/DrewCrouch1/Sentinel-Live-Attack-Lab/assets/158229796/a7b66804-6e76-4b97-9dfc-f94c324c0a8c)


### Notes:
Due to API limitations, the ipgeolocation.io API has a daily limit of 1,000 requests. Exercise caution to avoid exceeding this limit.

