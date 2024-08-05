# Elastic SIEM with Sysmon Integration

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
  <br />
   <strong>Logs:</strong> Windows logs that need to be analyzed are identified<br />
   <strong>Logstash:</strong> Collect logs and events data. It even parses and transforms data<br />
   <strong>Elastic Search:</strong> The transformed data from Logstash is store, search, and indexed<br />
   <strong>Kibana:</strong> Kibana uses Elasticsearch DB to explore, visualize, and share<br />
  <br />
   <img src="https://github.com/user-attachments/assets/1744ca96-0707-4b47-b01a-90f3c99ba065" alt="Project Overview"/>
   <p align="center">Simple Architecture of ELK Stack
  <br />
  <br />
    First, create account in Elastic and login to Elastic Cloud console, then navigate to "Integrations" under "Management" tab
    <img src="https://github.com/user-attachments/assets/e190467d-bc8e-4640-8d98-6f521036414b" alt="Integrations"/>
  <br />
  <br />
    Choose Elastic Defend
    <img src="https://github.com/user-attachments/assets/7bb6d632-819f-44d5-89f6-178a7317070c" alt="Elastic Defend"/>
  <br />
  <br />
    Click "Add Elastic Defend" button
    <img src="https://github.com/user-attachments/assets/dc7468a0-d8ce-4ff0-937c-f6b40a6ed3ed" alt="Add Elastic Defend"/>
  <br />
  <br />
    Select enrollent token and prepare new Windows 10 Virtual Machine in Virtual Box
    <img src="https://github.com/user-attachments/assets/d7cf9e61-0f1f-40b0-a87c-ba924d74217a" alt="Add Elastic Agent"/>
  <br />
  <br />
    In the Windows virtual machine, open powershell as administrator and run the command from Elastic web portal to install Elastic agent
    <img src="https://github.com/user-attachments/assets/b4509fd1-cad8-4506-83d9-048348e28c92" alt="Install Elastic Agent"/>
  <br />
  <br />
    Confirmed the enrollment agent has been enrolled and able to receive data from the Elastic web portal
    <img src="https://github.com/user-attachments/assets/5973a78b-894a-427e-b673-3764502cc2dd" alt="Agent Enrollment"/>
    <img src="https://github.com/user-attachments/assets/544c0e9c-fc67-4a94-aae4-3a9542726a22" alt="Windows Health" />
  <br />
  <br />
    Download Sysmon installer from Microsoft homepage and install in the VM

    https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
  <br />
    <img src="https://github.com/user-attachments/assets/c3f6d04b-f33b-4ba7-8aa7-689b3a916511" alt="Install Sysmon" />
  <br />
  <br />
    In order to collect the logs from Sysmon, we will need to add Windows integration in Agent Policy. Choose "Agent Policy 1", click "Add Integration" and search for "Windows"
    <img src="https://github.com/user-attachments/assets/eeef1d32-7967-4c24-9ce7-e9121c728ca1" alt="Agent Policy 1" />
    <img src="https://github.com/user-attachments/assets/600cac05-13c7-466e-aede-11109da1d274" alt="Add Integration" />
    <img src="https://github.com/user-attachments/assets/41c3e780-c8bb-4488-8cb5-cbaff6f6ae01" alt="Windows Integration" />
  <br />
  <br />
   Configure windows integration settings and make sure "Sysmon Operational" is turn on
   <img src="https://github.com/user-attachments/assets/dc355c9b-fc33-4d57-9995-1aba538eeb83" alt="Configure Integration" />
   <img src="https://github.com/user-attachments/assets/39889fbd-e4e6-4ee7-9cd0-bb947c18e6f3" alt="Sysmon Operational" />
  <br />
  <br />
   Return back to virtual machine, install Nmap and run scan to create logs
   <img src="https://github.com/user-attachments/assets/bceea907-8ff8-4929-925d-76e5c809019a" alt="Nmap Scan" />
  <br />
  <br />
   Go to "Logs" tab under "Observability".  In the search bar under “Stream” type in KQL command below to display the Nmap events created on your Windows VM
    
    process.args: "nmap"

   <img src="https://github.com/user-attachments/assets/50d579cb-09e7-4878-85df-b13b7b0eb2dd" alt="Nmap logs" />
  <br />
  <br />
   Go to "Analytics" > "Discover" tab and change data views to "logs-*". We can filter the logs received by using KQL syntax or user interface
   <img src="https://github.com/user-attachments/assets/af20b93d-492c-45c0-ad36-2252fa9e3f0e" alt="Discover" />
   


  <br />
  <br />
  <br />
  <br />
