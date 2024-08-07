# Elastic SIEM with Sysmon Integration

<h2>Description</h2>
Elastic SIEM provides a powerful and scalable solution for collecting and analyzing logs from Sysmon (System Monitor) across multiple endpoints, providing a unified view of system activities accross multiple resources. 
By integrating Sysmon with Elastic SIEM, organizations can gain enhanced visibility into system activities, enabling real-time detection and response to security threats.
This project focus on setting up Elastic Stack Security Information and Event Management (SIEM) home lab using the Elastic Web portal and a Windows virtual machine (VM) to generate and analyze security events, set up agents for log forwarding, create dashboards, and establish security alerts.
<br />

<h2>Utilities Used</h2>

- <b>VirtualBox</b>
- <b>Elastic Web Portal</b>
- <b>Nmap</b>

<h2>Environments Used </h2>

- <b>Elastic SIEM</b>
- <b>Windows 10 Pro (22H2)</b> 

<h2>Lab walk-through:</h2>
 <strong> Project Overview: </strong><br />
  <br />
   This project focusing on using a couple of key components of Elastic Stack:-<br />
  <br />
   <strong>Logs:</strong> Windows logs that need to be analyzed are identified<br />
   <strong>Logstash:</strong> Collects logs and event data. It also parses and transforms the data<br />
   <strong>Elastic Search:</strong> The transformed data from Logstash is stored, searched, and indexed in Elastic Search<br />
   <strong>Kibana:</strong> Kibana uses the Elasticsearch database to explore, visualize, and share the data<br />
  <br />
   <img src="https://github.com/user-attachments/assets/1744ca96-0707-4b47-b01a-90f3c99ba065" alt="Project Overview"/>
<p align="center">Simple Architecture of ELK Stack
  <br />
  <br />
    First, create account in Elastic and login to Elastic Cloud console, then navigate to "Integrations" under "Management" tab
    <img width="90%" src="https://github.com/user-attachments/assets/e190467d-bc8e-4640-8d98-6f521036414b" alt="Integrations"/>
  <br />
  <br />
    Choose Elastic Defend
    <img width="90%" height="80%" src="https://github.com/user-attachments/assets/7bb6d632-819f-44d5-89f6-178a7317070c" alt="Elastic Defend"/>
  <br />
  <br />
    Click "Add Elastic Defend" button
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/dc7468a0-d8ce-4ff0-937c-f6b40a6ed3ed" alt="Add Elastic Defend"/>
  <br />
  <br />
    Select enrollent token and prepare new Windows 10 Virtual Machine in Virtual Box
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/d7cf9e61-0f1f-40b0-a87c-ba924d74217a" alt="Add Elastic Agent"/>
  <br />
  <br />
    In the Windows virtual machine, open powershell as administrator and run the command from Elastic web portal to install Elastic agent
    <img width="85%" height="85%" src="https://github.com/user-attachments/assets/b4509fd1-cad8-4506-83d9-048348e28c92" alt="Install Elastic Agent"/>
  <br />
  <br />
    Confirmed the enrollment agent has been enrolled and able to receive data from the Elastic web portal
    <img width="50%" height="50%" src="https://github.com/user-attachments/assets/5973a78b-894a-427e-b673-3764502cc2dd" alt="Agent Enrollment"/>
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/544c0e9c-fc67-4a94-aae4-3a9542726a22" alt="Windows Health" />
  <br />
  <br />
    Download Sysmon installer from Microsoft homepage and install in the VM

    https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
  <br />
    <img width="90%" src="https://github.com/user-attachments/assets/c3f6d04b-f33b-4ba7-8aa7-689b3a916511" alt="Install Sysmon" />
  <br />
  <br />
    <p align="center"> In order to collect the logs from Sysmon, we will need to add Windows integration in Agent Policy. Choose "Agent Policy 1", click "Add Integration" and search for "Windows"
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/d16963f8-949b-4670-9d9f-10e2f7050aac" alt="Agent Policy 1" />
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/651c4e53-5421-4514-8977-41d593b2f48e" alt="Add Integration" />
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/73ffdc52-bb4a-4f96-9b23-15fef347c98f" alt="Windows Integration" />
  <br />
  <br />
   Configure windows integration settings and make sure "Sysmon Operational" is turn on
   <img width="60%" height="60%" src="https://github.com/user-attachments/assets/dc355c9b-fc33-4d57-9995-1aba538eeb83" alt="Configure Integration" />
   <img width="60%" src="https://github.com/user-attachments/assets/39889fbd-e4e6-4ee7-9cd0-bb947c18e6f3" alt="Sysmon Operational" />
  <br />
  <br />
   Return back to virtual machine, install Nmap and run scan to create some logs
   <img width="90%" src="https://github.com/user-attachments/assets/bceea907-8ff8-4929-925d-76e5c809019a" alt="Nmap Scan" />
  <br />
  <br />
   In Elastic web portal, go to "Logs" tab under "Observability".  In the search bar under “Stream”, type in KQL command below to display the Nmap events created by Windows VM
    
    process.args: "nmap"

   <img src="https://github.com/user-attachments/assets/50d579cb-09e7-4878-85df-b13b7b0eb2dd" alt="Nmap logs" />
  <br />
  <br />
   <p align="center">To create a dashboard to visualize the events, click "Dashboards" and then "Create Visualization"
   <img width="90%" src="https://github.com/user-attachments/assets/28300455-0aad-491f-9581-def212a5073c" alt="Dashboards" />
  <br />
  <br />
   Filter using KQL syntax or add the field names
   <img src="https://github.com/user-attachments/assets/0c94b6e0-548f-4f96-9c19-8c5be3cd6299" alt="Visualization" />
  <br />
  <br />
   To create alerts, go to Security > Rules
  <br />
   <img width="20%" height="20%" src="https://github.com/user-attachments/assets/e754f5b8-c8b1-42dc-b415-9e21c1145407" alt="Security Rules Tab" />
  <br />
  <br />
   Click 'Detection rules (SIEM)'
   <img width="80%" height="90%" src="https://github.com/user-attachments/assets/c921e51f-fd28-4e9c-b375-83fed366f094" alt="Detection Rules" />
  <br />
  <br />
   Create new rule from button on the top right corner
   <img width="80%" height="80%" src="https://github.com/user-attachments/assets/f6134c26-a7b4-4cf8-b42e-b4c22d87ed0b" alt="New rule" />
  <br />
  <br />
    Choose custom query and add KQL query
  <br />
    <img width="70%" height="65%" src="https://github.com/user-attachments/assets/9fa8d039-1112-416f-b2bf-3e4fc206ecb1" alt="Custom query" />
  <br />
  <br />
    Insert alert name and set the severity/risk score
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/77590232-a45f-43e0-bda9-1df94d0fe26a" alt="Alert name" />
  <br />
  <br />
    Set the schedule rule to run periodically
  <br />
    <img width="70%" height="70%" src="https://github.com/user-attachments/assets/57fe67f8-072b-42dd-936d-2ae7e9fca41d" alt="Schedule rule" />
  <br />
  <br />
    Set the rule actions if the alert generated so that you can alert the analysts
    <img width="70%" height="70%" src="https://github.com/user-attachments/assets/ec24d6fa-f116-431d-a596-356711100354" alt="Rule actions" />
  <br />
  <br />
    Example alert generated in the portal and sent to the email
    <img width="120%" height="120%"src="https://github.com/user-attachments/assets/c6785869-f34a-4b73-bdff-a263eaceefde" alt="Example alert" />
    <img src="https://github.com/user-attachments/assets/9a99a34d-a744-415f-8d2c-89ff5c8bb072" alt="Email" />
  <br />
  <br />
  <br />
  <br />
</p>
