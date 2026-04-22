### Scenario
An alert from the Intrusion Detection System (IDS) flagged suspicious lateral movement activity involving PsExec. This indicates potential unauthorized access and movement across the network. As a SOC Analyst, your task is to investigate the provided PCAP file to trace the attacker’s activities. Identify their entry point, the machines targeted, the extent of the breach, and any critical indicators that reveal their tactics and objectives within the compromised environment.

### Q1 To effectively trace the attacker's activities within our network, can you identify the IP address of the machine from which the attacker initially gained access?
Navigate to Statistics → Conversations. In the IPv4 section, you can observe a suspicious IP address generating a high volume of packets.
<img width="1920" height="1080" alt="Screenshot (322)" src="https://github.com/user-attachments/assets/b1e1030b-2e1d-49c8-b699-aca1cc302815" />
### Answer: 10.0.0.130

### Q2 To fully understand the extent of the breach, can you determine the machine's hostname to which the attacker first pivoted?
Follow TCP stream
<img width="1920" height="1080" alt="Screenshot (323)" src="https://github.com/user-attachments/assets/6ce17ebf-e3eb-4e7a-af6a-1e2a86809ff3" />
### Answer: Sales-PC

### Q3 Knowing the username of the account the attacker used for authentication will give us insights into the extent of the breach. What is the username utilized by the attacker for authentication?
On SMB2 packet, I saw that ssales user was the account of this session
<img width="1920" height="1080" alt="Screenshot (324)" src="https://github.com/user-attachments/assets/d4a3c8dc-5708-4979-9042-9fc777f49022" />
### Answer: ssales

### Q4 After figuring out how the attacker moved within our network, we need to know what they did on the target machine. What's the name of the service executable the attacker set up on the target?
<img width="1920" height="1080" alt="Screenshot (325)" src="https://github.com/user-attachments/assets/e707dbee-376b-4a02-ac4f-9237d912834d" />
### Answer: psexesvc.exe

### Q5 We need to know how the attacker installed the service on the compromised machine to understand the attacker's lateral movement tactics. This can help identify other affected systems. Which network share was used by PsExec to install the service on the target machine?
<img width="1920" height="1080" alt="Screenshot (326)" src="https://github.com/user-attachments/assets/04734074-7998-4295-be37-2ed1533230f3" />
### Answer: ADMIN$

### Q6 We must identify the network share used to communicate between the two machines. Which network share did PsExec use for communication?
<img width="1920" height="1080" alt="Screenshot (326)" src="https://github.com/user-attachments/assets/04734074-7998-4295-be37-2ed1533230f3" />
### Answer: IPC$

### Q7 Now that we have a clearer picture of the attacker's activities on the compromised machine, it's important to identify any further lateral movement. What is the hostname of the second machine the attacker targeted to pivot within our network?
<img width="1323" height="326" alt="1_daKsV4jTmJvf3Ugi0mutOg" src="https://github.com/user-attachments/assets/5da30697-c70f-4b06-a273-f0df460744fe" />
### Answer: Marketing-PC
