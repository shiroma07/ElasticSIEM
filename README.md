# Elastic SIEM with Sysmon Integration

<h2>Description</h2>
Elastic SIEM provides a powerful and scalable solution for collecting and analyzing logs from Sysmon (System Monitor) across multiple endpoints, providing a unified view of system activities across multiple resources. 
By integrating Sysmon with Elastic SIEM, organizations can gain enhanced visibility into system activities, enabling real-time detection and response to security threats.
This project focuses on setting up an Elastic Stack Security Information and Event Management (SIEM) home lab using the Elastic Web portal and a Windows virtual machine (VM). The setup includes generating and analyzing security events, configuring Elastic agents for log forwarding, creating dashboards, and establishing security alerts.
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
   This project focusing on using a couple of key components from Elastic Stack:-<br />
  <br />
   <strong>Logs:</strong> Identify the Windows logs that need to be analyzed<br />
   <strong>Logstash:</strong> Collects logs and event data, and then parses and transforms the data<br />
   <strong>Elastic Search:</strong> The transformed data from Logstash is stored, searched, and indexed in Elastic Search<br />
   <strong>Kibana:</strong> Uses the data in Elastic search database to explore, visualize, and share the data<br />
  <br />
   <img src="https://github.com/user-attachments/assets/1744ca96-0707-4b47-b01a-90f3c99ba065" alt="Project Overview"/>
   <p align="center">Simple Architecture of ELK Stack
  <br />
  <br />
  <br />
<b>Step 1: Create an Elastic account and add Elastic Agent to the Windows virtual machine</b>
  <br />
  <br />   
    Create account in Elastic and log in to Elastic Cloud console. Then, navigate to the "Integrations" section under the "Management" tab
    <img width="90%" src="https://github.com/user-attachments/assets/e190467d-bc8e-4640-8d98-6f521036414b" alt="Integrations"/>
  <br />
  <br />
    Select "Elastic Defend" from the list of available integrations
    <img width="90%" height="80%" src="https://github.com/user-attachments/assets/7bb6d632-819f-44d5-89f6-178a7317070c" alt="Elastic Defend"/>
  <br />
  <br />
    Click the "Add Elastic Defend" button
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/dc7468a0-d8ce-4ff0-937c-f6b40a6ed3ed" alt="Add Elastic Defend"/>
  <br />
  <br />
    Select the enrollment token, and then set up a new Windows 10 virtual machine in VirtualBox
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/d7cf9e61-0f1f-40b0-a87c-ba924d74217a" alt="Add Elastic Agent"/>
  <br />
  <br />
    In Windows virtual machine, open PowerShell as an administrator and run command provided in the Elastic web portal to install Elastic agent
  <br />
    <img width="85%" height="85%" src="https://github.com/user-attachments/assets/b4509fd1-cad8-4506-83d9-048348e28c92" alt="Install Elastic Agent"/>
  <br />
  <br />
    Confirm that the Elastic Agent has been successfully enrolled and is able to receive data from the Elastic web portal
    <img width="50%" height="50%" src="https://github.com/user-attachments/assets/5973a78b-894a-427e-b673-3764502cc2dd" alt="Agent Enrollment"/>
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/544c0e9c-fc67-4a94-aae4-3a9542726a22" alt="Windows Health" />
  <br />
  <br />
    <b>Step 2: Integrate Sysmon to Elastic web portal</b>
  <br />
  <br />
    Download Sysmon installer from Microsoft homepage and install it on the virtual machine

    https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
  <br />
    <img width="90%" src="https://github.com/user-attachments/assets/c3f6d04b-f33b-4ba7-8aa7-689b3a916511" alt="Install Sysmon" />
  <br />
  <br />
    <p align="center"> To collect logs from Sysmon, you will need to add the Windows integration to your Agent Policy. Select "Agent Policy 1", click on "Add Integration", and then search for "Windows"
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/d16963f8-949b-4670-9d9f-10e2f7050aac" alt="Agent Policy 1" />
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/651c4e53-5421-4514-8977-41d593b2f48e" alt="Add Integration" />
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/73ffdc52-bb4a-4f96-9b23-15fef347c98f" alt="Windows Integration" />
  <br />
  <br />
   Configure the Windows integration settings and ensure that the "Sysmon Operational" option is turned on
   <img width="60%" height="60%" src="https://github.com/user-attachments/assets/dc355c9b-fc33-4d57-9995-1aba538eeb83" alt="Configure Integration" />
   <img width="60%" src="https://github.com/user-attachments/assets/39889fbd-e4e6-4ee7-9cd0-bb947c18e6f3" alt="Sysmon Operational" />
  <br />
  <br />
   <b>Step 3: Generate logs by using Nmap and view from Elastic Web Portal</b>
  <br />
  <br />
   Return to the virtual machine, install Nmap, and run a scan to generate some logs
   <img width="90%" src="https://github.com/user-attachments/assets/bceea907-8ff8-4929-925d-76e5c809019a" alt="Nmap Scan" />
  <br />
  <br />
   In the Elastic web portal, navigate to the "Logs" tab under "Observability." In the search bar under "Stream", type the following KQL command to display the Nmap events created by the Windows virtual machine
    
    process.args: "nmap"

   <img src="https://github.com/user-attachments/assets/50d579cb-09e7-4878-85df-b13b7b0eb2dd" alt="Nmap logs" />
  <br />
  <br />
   <p align="center"><b>Step 4: Create a dashboard</b>
  <br />
  <br />
   To create a dashboard for visualizing the events, click on "Dashboards" and then select "Create Visualization"
   <img width="90%" src="https://github.com/user-attachments/assets/28300455-0aad-491f-9581-def212a5073c" alt="Dashboards" />
  <br />
  <br />
   Filter the data using KQL syntax or by adding the field names on the left tab. The dashboards provide a real-time view of critical metrics and events, allowing for immediate detection of issues or security threats.
   Visualization helps in identifying patterns, trends, and anomalies that might not be apparent in raw data
   <img src="https://github.com/user-attachments/assets/03f2165e-9bc7-454f-b980-fd57fb31b02b" alt="Visualization" />
  <br />
  <br />
    <b>Step 5: Create an alert and notify through email</b>
  <br />
  <br />
    Alerts serve as early warnings for unusual or suspicious activity, allowing for proactive measures before issues escalate. To create alerts, navigate to "Security" and then select "Rules"
  <br />
   <img width="20%" height="20%" src="https://github.com/user-attachments/assets/e754f5b8-c8b1-42dc-b415-9e21c1145407" alt="Security Rules Tab" />
  <br />
  <br />
   Click on "Detection rules (SIEM)"
   <img width="80%" height="90%" src="https://github.com/user-attachments/assets/c921e51f-fd28-4e9c-b375-83fed366f094" alt="Detection Rules" />
  <br />
  <br />
   Create a new rule by clicking the button in the top right corner
   <img width="80%" height="80%" src="https://github.com/user-attachments/assets/f6134c26-a7b4-4cf8-b42e-b4c22d87ed0b" alt="New rule" />
  <br />
  <br />
    Choose "Custom Query" and add your KQL query
  <br />
    <img width="70%" height="65%" src="https://github.com/user-attachments/assets/9fa8d039-1112-416f-b2bf-3e4fc206ecb1" alt="Custom query" />
  <br />
  <br />
    Insert the alert name and set the severity or risk score as appropriate
    <img width="80%" height="80%" src="https://github.com/user-attachments/assets/382ed3fb-d94f-44f1-99d4-cb2316c88595" alt="Alert name" />
  <br />
  <br />
    Set the schedule for the rule to run periodically
  <br />
    <img width="70%" height="70%" src="https://github.com/user-attachments/assets/57fe67f8-072b-42dd-936d-2ae7e9fca41d" alt="Schedule rule" />
  <br />
  <br />
    Configure the rule actions to specify how alerts should be handled if triggered, ensuring that notifications are sent to the analysts
  <br />
    <img width="70%" height="70%" src="https://github.com/user-attachments/assets/ec24d6fa-f116-431d-a596-356711100354" alt="Rule actions" />
  <br />
  <br />
    Example of an alert generated in the portal and sent via email for timely detection of issues
    <img width="140%" height="140%"src="https://github.com/user-attachments/assets/9da5301b-c2f6-400a-9829-3ad9f1f41210" alt="Example alert" />
    <img src="https://github.com/user-attachments/assets/be64aefb-deaa-4dcb-a706-502042cdebda" alt="Email" />
  <br />
  <br />
  <br />
  <br />
</p>
