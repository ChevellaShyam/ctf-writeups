### Scenario
A large multinational corporation heavily relies on the 3CX software for phone communication, making it a critical component of their business operations. After a recent update to the 3CX Desktop App, antivirus alerts flag sporadic instances of the software being wiped from some workstations while others remain unaffected. Dismissing this as a false positive, the IT team overlooks the alerts, only to notice degraded performance and strange network traffic to unknown servers. Employees report issues with the 3CX app, and the IT security team identifies unusual communication patterns linked to recent software updates.

As the threat intelligence analyst, it's your responsibility to examine this possible supply chain attack. Your objectives are to uncover how the attackers compromised the 3CX app, identify the potential threat actor involved, and assess the overall extent of the incident. 

### File Hash : 59e1edf4d82fae4978e97512b0331b7eb21dd4b838b850ba46794d9c7a2c0983

### Q1 Understanding the scope of the attack and identifying which versions exhibit malicious behavior is crucial for making informed decisions if these compromised versions are present in the organization. How many versions of 3CX running on Windows have been flagged as malware?
- In late March, 2023, a software supply chain compromise spread malware via a trojanized version of 3CX’s legitimate software that was available to download from their website. 3CX Desktop App is enterprise software that provides communications for its users including chat, video calls, and voice calls. This is the first time Mandiant has seen a software supply chain attack lead to another software supply chain attack. According to Huntress and 3CX’s released notifications, the currently known affected 3CX DesktopApp versions are:

- 18.12.407
- 18.12
### Answer: 2

### Q2 Determining the age of the malware can help assess the extent of the compromise and track the evolution of malware families and variants. What's the UTC creation time of the .msi malware?
- Uploading the MSI file to VirusTotal shows the file has been flagged as malicious by the community.
VirusTotal provides the history of the MSI file under the details tab, including the Creation Time.
<img width="1920" height="1080" alt="Screenshot (198)" src="https://github.com/user-attachments/assets/271ddba6-9354-4989-8a5a-f4cbf39f312a" />
### Answer : 2023-03-13 06:33

### Q3 Executable files (.exe) are frequently used as primary or secondary malware payloads, while dynamic link libraries (.dll) often load malicious code or enhance malware functionality. Analyzing files deposited by the Microsoft Software Installer (.msi) is crucial for identifying malicious files and investigating their full potential. Which malicious DLLs were dropped by the .msi file?
- Under the relations tab on VirusTotal, we can see two .dll files bundled by the malicious file.
  <img width="640" height="210" alt="1_yR7dOd4J6m-SQlJe9b8d3Q" src="https://github.com/user-attachments/assets/72f97cd9-0a03-4bb4-bea5-ac06a5a225e3" />

### Answer: ffmpeg.dll,d3dcompiler_47.dll

### Q4 Recognizing the persistence techniques used in this incident is essential for current mitigation strategies and future defense improvements. What is the MITRE Technique ID employed by the .msi files to load the malicious DLL?
- There are a number of different attack types, such as Execution and Defense Evasion, but under Privilege Escalation, we can see the technique ID for ‘Hijack Execution Flow’, which is T1547. There is also another ID, T1574.002 for DLL Side-Loading, which confirms this is the correct ID.
<img width="614" height="640" alt="1_Fh6Cct8hBFvEoyLOlzHbhw" src="https://github.com/user-attachments/assets/30b880d1-2e3c-432c-bce9-3aa5a700c7ef" />
### Answer: T1574

### Q5 Recognizing the malware type (threat category) is essential to your investigation, as it can offer valuable insight into the possible malicious actions you'll be examining. What is the threat category of the two malicious DLLs?
- Going back to the detect ion tab we can see they are trojans.
- <img width="1920" height="1080" alt="Screenshot (199)" src="https://github.com/user-attachments/assets/710c4106-5b52-418c-a122-4c3cc7c5e61d" />

### Answer: Trojan

### Q6 As a threat intelligence analyst conducting dynamic analysis, it's vital to understand how malware can evade detection in virtualized environments or analysis systems. This knowledge will help you effectively mitigate or address these evasive tactics. What is the MITRE ID for the virtualization/sandbox evasion techniques used by the two malicious DLLs?
- Back to the behaviour tab, and under Defense Evasion MITRE ATT&CK’s we can see Virtualisation/Sandbox Evasion — T1497
<img width="1581" height="825" alt="1_PLs6nw7u56pZizlUaX6YMQ" src="https://github.com/user-attachments/assets/7c307dd7-fcb9-446d-a4ab-cef5a6e1419e" />
### Answer: T1497

### Q7 When conducting malware analysis and reverse engineering, understanding anti-analysis techniques is vital to avoid wasting time. Which hypervisor is targeted by the anti-analysis techniques in the ffmpeg.dll file?
- Going back to the ffmpeg.dll’s VirusTotal page, navigate to the Defense Evasion MITRE ATT&CK’s and we can see the file references anti-VM strings targeting VMWare.
<img width="583" height="784" alt="1_8cgKpLWm2T7pWRqePDV9PQ" src="https://github.com/user-attachments/assets/4e63a02b-370b-4484-8bbb-4139b9975997" />
### Answer: VMware

### Q8 Identifying the cryptographic method used in malware is crucial for understanding the techniques employed to bypass defense mechanisms and execute its functions fully. What encryption algorithm is used by the ffmpeg.dll file?
-Again, under Defense Evasion tactics, we can see the ffmpeg.dll file encrypts data using RC4 KSA and RC4 PRGA, so the answer is RC4.
<img width="609" height="704" alt="1_8cgKpLWm2T7pWRqePDV9PQ" src="https://github.com/user-attachments/assets/b6c37006-7189-4673-a702-f0423867874d" />
### ANswer: RC4

### 9Q As an analyst, you've recognized some TTPs involved in the incident, but identifying the APT group responsible will help you search for their usual TTPs and uncover other potential malicious activities. Which group is responsible for this attack?
- With some research and using google search engine i got
<img width="1918" height="699" alt="Screenshot 2025-11-05 162443" src="https://github.com/user-attachments/assets/a3ab494d-5143-419b-b5f1-14ed54ba2a4a" />
### Answer: Lazarus
