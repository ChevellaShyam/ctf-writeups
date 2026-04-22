### Scenario
You are part of the Threat Intelligence team in the SOC (Security Operations Center). An executable file has been discovered on a colleague's computer, and it's suspected to be linked to a Command and Control (C2) server, indicating a potential malware infection.
Your task is to investigate this executable by analyzing its hash. The goal is to gather and analyze data beneficial to other SOC members, including the Incident Response team, to respond to this suspicious behavior efficiently.

### Q1 Categorizing malware enables a quicker and clearer understanding of its unique behaviors and attack vectors. What category has Microsoft identified for that malware in VirusTotal?

<img width="1920" height="1080" alt="Screenshot (157)" src="https://github.com/user-attachments/assets/d0e442b6-321b-4cd5-9978-e39eba47cc93" />

### Answer: Trojan

### Q2 Clearly identifying the name of the malware file improves communication among the SOC team. What is the file name associated with this malware?

<img width="1920" height="1080" alt="Screenshot (158)" src="https://github.com/user-attachments/assets/cce0fe6a-db35-41bb-a94a-c09d64a7e61e" />

### Answer: Wextract

### Q3 Knowing the exact timestamp of when the malware was first observed can help prioritize response actions. Newly detected malware may require urgent containment and eradication compared to older, well-documented threats. What is the UTC timestamp of the malware's first submission to VirusTotal?

<img width="1920" height="1080" alt="Screenshot (159)" src="https://github.com/user-attachments/assets/1fabfcec-3e20-4fca-a4ff-94b048c186a7" />
### Answer: 2023-10-06 04:41

### Q4 Understanding the techniques used by malware helps in strategic security planning. What is the MITRE ATT&CK technique ID for the malware's data collection from the system before exfiltration?

<img width="1920" height="1080" alt="Screenshot (160)" src="https://github.com/user-attachments/assets/09c60bde-f7ed-410c-a301-cbe7d219773b" />
### Answer: T1005

### Q5 Following execution, which social media-related domain names did the malware resolve via DNS queries?
<img width="1920" height="1080" alt="Screenshot (161)" src="https://github.com/user-attachments/assets/c163817d-44e6-4840-9d43-15d111cc01b8" />
### Answer: facebook.com

### Q6 Once the malicious IP addresses are identified, network security devices such as firewalls can be configured to block traffic to and from these addresses. Can you provide the IP address and destination port the malware communicates with?
<img width="1920" height="1080" alt="Screenshot (162)" src="https://github.com/user-attachments/assets/181ed780-59a5-47a2-b561-3f4c20569e1c" />
### Answer: 77.91.124.55:19071

### Q7 YARA rules are designed to identify specific malware patterns and behaviors. Using MalwareBazaar, what's the name of the YARA rule created by "Varp0s" that detects the identified malware?
  <img width="1920" height="1080" alt="Screenshot (163)" src="https://github.com/user-attachments/assets/5c7c331b-277d-47d6-8bb4-a9d42f330ab3" />
### Answer: detect_Redline_Stealer

### Q8 Understanding which malware families are targeting the organization helps in strategic security planning for the future and prioritizing resources based on the threat. Can you provide the different malware alias associated with the malicious IP address according to ThreatFox?
<img width="1920" height="1080" alt="Screenshot (164)" src="https://github.com/user-attachments/assets/b818287e-3cee-4453-af16-b5cac7d24d47" />
### Answer: RECORDSTEALER

### Q9 By identifying the malware's imported DLLs, we can configure security tools to monitor for the loading or unusual usage of these specific DLLs. Can you provide the DLL utilized by the malware for privilege escalation?
<img width="1920" height="1080" alt="Screenshot (165)" src="https://github.com/user-attachments/assets/dfc76f70-b9b7-4579-9dea-f26458820711" />
### Answer: ADVAPI32.dll
