# Elastic SIEM with Sysmon Personal Lab

<h2>Description</h2>
Elastic SIEM provides a powerful and scalable solution for collecting and analyzing logs from Sysmon (System Monitor) across multiple endpoints, providing a unified view of system activities accross multiple resources. 
By integrating Sysmon with Elastic SIEM, organizations can gain enhanced visibility into system activities, enabling real-time detection and response to security threats.
This project focus on setting up Elastic Stack Security Information and Event Management (SIEM) home lab using the Elastic Web portal and a Windows virtual machine (VM) to generate and analyze security events, set up agents for log forwarding, create dashboards, and establish security alerts.
<br />

<h2>Utilities Used</h2>

- <b>VirtualBox</b>
- <b>Elastic Web Portal</b>

<h2>Environments Used </h2>

- <b>Elastic SIEM</b>
- <b>Windows 10 Pro (22H2)</b> 

<h2>Lab walk-through:</h2>
 <strong> Project Overview: </strong><br />
   <br />
   This project focusing on using a couple of key components of Elastic Stack:-<br />
   <strong>Logs:</strong> Windows logs that need to be analyzed are identified<br />
   <strong>Logstash:</strong> Collect logs and events data. It even parses and transforms data<br />
   <strong>Elastic Search:</strong> The transformed data from Logstash is store, search, and indexed<br />
   <strong>Kibana:</strong> Kibana uses Elasticsearch DB to explore, visualize, and share<br />
 <br />
   <img src="https://github.com/user-attachments/assets/1744ca96-0707-4b47-b01a-90f3c99ba065" alt="Project Overview"/>
   <p align="center">Simple Architecture of ELK Stack
 <br />
 <br />
    Create account in Elastic and login to Elastic Cloud console, then navigate to "Integrations" under "Management" tab
    <img src="https://github.com/user-attachments/assets/e190467d-bc8e-4640-8d98-6f521036414b" alt="Project Overview"/>
    Choose Elastic Defend
    <img src="https://github.com/user-attachments/assets/e190467d-bc8e-4640-8d98-6f521036414b" alt="Project Overview"/>
    Install Windows 10 Pro in Virtual Box, and open
