# 30-Days-SOC-Challenge-HOME-LAB-

## Objective
The SOC Home Lab project aimed to create a comprehensive environment for simulating, detecting, and responding to cyber-attacks. The primary focus was to set up a fully functional Security Operations Center (SOC) infrastructure using VMware Workstation 17, configure various security tools, and perform attack simulations. This hands-on experience was designed to enhance understanding of SOC operations, attack detection, incident response, and security tool integration.

### Skills Learned
- Proficiency in setting up and configuring virtual environments using VMware Workstation 17.
- Advanced understanding of SIEM concepts and practical application with ELK stack.
- Expertise in deploying and managing Command and Control (C2) infrastructure.
- Ability to perform and analyze attack simulations using tools like Mythic.
- Enhanced knowledge of Windows and Linux server administration.
- Proficiency in configuring and using endpoint detection and response (EDR) tools.
- Development of skills in creating and managing security alerts and dashboards.
- Experience in setting up and integrating ticketing systems for incident management.
- Improved incident investigation and threat-hunting capabilities.
- Enhanced understanding of the MITRE ATT&CK framework and its application.

### Tools Used
- VMware Workstation 17 for virtualization.
- ELK stack (Elasticsearch, Logstash, Kibana) for SIEM functionality.
- Mythic C2 framework for command and control simulation.
- Sysmon for enhanced Windows system monitoring.
- Elastic Agent and Fleet Server for centralized agent management.
- osTicket for ticketing system implementation.
- Elastic Defend for endpoint detection and response.
- Windows Server 2022 and Ubuntu Server 24.02 as target machines.
- Kali Linux as an attack box.

## Steps

Insights and Review of the Challenge

By doing this challenge, I learned and gained valuable hands-on experience in setting and configuring a SOC home lab deployed on VMWare workstation 17, a C2 server running Mythic, performing attacks on my target endpoints, investigating and configuring alerts, setting up a Ticketing system, and making my dashboards.

It also taught me the importance of documenting what I learned so I could further understand my thought process while doing the tasks. This was also helpful since I could look back on the concepts that I learned.

**Documentation and diagrams:**

[Logical Diagram](https://medium.com/@deepshah.201199/1-30-soc-analyst-challenge-6f1f3a824c090)

[Attack Diagram](https://medium.com/@deepshah.201199/19-20-soc-analyst-challenge-6379535ca58a)

Creating a logical diagram helps visualize and further understand the data flow and the infrastructure that will be configured for the project.
![image](https://github.com/user-attachments/assets/f49ff426-951a-48d2-be5f-29ad38a2f45e)


The attack diagram serves to visualize the tasks to be performed during the attack simulation by mapping out how to attack the target machine. Each tasks were grouped into phases that matched with tactics found in the MITRE ATT&CK Framework.
![image](https://github.com/user-attachments/assets/6f434b41-eef7-446d-a6ef-db544bbacc84)


**Deployment of ELK instance**

[Installing Elasticsearch](https://medium.com/@deepshah.201199/3-30-soc-analyst-challenge-b12a2653b77f)

[Installing Kibana](https://medium.com/@deepshah.201199/4-30-soc-analyst-challenge-697c6f426d1c)

Using an Ubuntu server, an ELK instance was configured as an SIEM on the VMware Workstation 17. Where ElasticSearch is used to store and query logs/telemetry, and Kibana to access ElasticSearch in a Web GUI.

Kibana acts as a data visualization and exploration tool that integrates with Elasticsearch. It allows users to create visualizations, and dashboards, and perform complex queries to gain insights from their data.

**Windows and Ubuntu Target Machines**

[Deploying Windows Server-22](https://medium.com/@deepshah.201199/6-30-soc-analyst-challenge-5f9c8494167f)

[Deploying Ubuntu Server 24.02](https://medium.com/@deepshah.201199/12-30-soc-analyst-challenge-c44002865276)

[Installing Sysmon on Windows Server](https://medium.com/@deepshah.201199/9-30-soc-analyst-challenge-4ecac2e4b695)

Both servers are deployed on VMware Workstation 17 to act as target machines for the project. Both SSH and RDP protocols were exposed to the internet to be able to gather brute-force telemetry for investigations. Both servers will also be used during the attack simulation using Mythic.

**Installing Fleet Server and Elastic Agent**

[Elastic agent and Fleet server setup, install Elastic agent to Windows Server](https://medium.com/@deepshah.201199/7-30-soc-analyst-challenge-34dd9dffa61a)

[Ingest Sysmon and Windows Defender logs into ElasticSearch](https://medium.com/@deepshah.201199/10-30-soc-analyst-challenge-d7ed6cf0fc67)

[Install Elastic Agent into the Ubuntu Server](https://medium.com/@deepshah.201199/13-30-soc-analyst-challenge-70336bb0467e)

A Fleet server was deployed on an Ubuntu server on VMware Workstation 17, a fleet server is used for the centralized management of agents. This makes managing Elastic agents simple and scalable, promoting consistency when it comes to configurations across all agents.

Elastic agent was used to forward endpoint telemetry from both the Windows and Ubuntu servers to ElasticSearch. Allowing for log data and endpoint telemetry to be queried and used through the Elastic Web GUI.

**Command and Control Server and Attack box**

[Mythic C2 Server setup](https://medium.com/@deepshah.201199/20-30-soc-analyst-challenge-c761f2c27f24)

[Apollo agent setup and attack simulation](https://medium.com/@deepshah.201199/21-30-soc-analyst-challenge-c0b93384e2c3)

Attack infrastructure is deployed on VMWare Workstation 17 where an Ubuntu server is used to run Mythic to act as a Command and Control server for the project. Apollo agent was chosen from the available Mythic agents and configured for affected endpoints to beacon out to the Mythic C2 server for commands.

Attack simulation is conducted on the Windows server through the use of the Mythic C2 server, Kali Linux attack box, and the attack diagram. The Windows server was successfully compromised, being able to exfiltrate sensitive data and run commands using the established C2 session.

**Creating Alerts and Dashboards**

[Creating an SSH brute force attack alert and dashboard](https://medium.com/@deepshah.201199/14-30-soc-analyst-challenge-2c73ac8142db)

[Creating an RDP brute force attack alert](https://medium.com/@deepshah.201199/16-30-soc-analyst-challenge-d9e20e049550)

[Creating an RDP brute force attack dashboard](https://medium.com/@deepshah.201199/17-30-soc-analyst-challenge-7dfc65cd1a4b)

[Creating an alert and dashboard for telemetry generated by Mythic](https://medium.com/@deepshah.201199/22-30-soc-analyst-challenge-b4ecad8d3a23)

Created SIEM rules on the Elastic Web GUI for SSH and RDP brute force attacks, and the existence of Mythic agent on an endpoint so that an alert will be generated whenever it is triggered.

Dashboards were created to provide a high-level overview and visualization of statistics based on existing telemetry related to Authentication attempts for RDP and SSH protocols, and suspicious activity.

**Configuring a Ticketing System using osTicket**

[Setting up osTicket](https://medium.com/@deepshah.201199/24-30-soc-analyst-challenge-3ca64463df13)

[Integrating osTicket into the ELK instance](https://medium.com/@deepshah.201199/25-30-soc-analyst-challenge-fd634e78e140)

A ticketing system is configured to track and create tickets when alerts are generated by Elastic. This is used to organize the handling of alerts by assigning tickets to agents who are going to handle them. This also provides an audit trail of tickets and actions taken which satisfies one of the A’s in the AAA in security, which is Audit and Accountability.

**Investigation**

[Investigating SSH Brute Force Attacks](https://medium.com/@deepshah.201199/26-30-soc-analyst-challenge-0d106392e192)

[Investigating RDP Brute Force Attacks](https://medium.com/@deepshah.201199/27-30-soc-analyst-challenge-7ed377497916)

[Investigating Mythic C2 Agent](https://medium.com/@deepshah.201199/28-30-soc-analyst-challenge-6818103e9651)

Learned and applied the methodologies used to detect and investigate incidents related to SSH and RDP brute force attacks and activities related to Command and Control. Applied best practices in correlating events and how to hunt for potential C2 activities.

**Installing Elastic Defend (EDR)**

[Configuring Elastic Defend](https://medium.com/@deepshah.201199/29-30-soc-analyst-challenge-659877e4635a)

Configured Elastic Defend to further secure endpoints within the network infrastructure. Tackled how to automate response whenever Elastic Endpoint Security alerts are generated and identified what kinds of telemetry Elastic Defend generates.

## Conclusion:

It is an understatement to say that I learned a lot during the span of this challenge, it has taught me both theoretical and valuable hands-on skills that I know that I can apply in my career in the future. At the end of the challenge, you are left with a SOC lab that you can use to further hone your skills, whether that be for detection, investigation, creating dashboards, attack simulation, or even configuring more integrations. It serves as a great introduction to anybody interested in jump-starting their career in cybersecurity.
