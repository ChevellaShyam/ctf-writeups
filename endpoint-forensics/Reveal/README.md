## Scenario
You are a forensic investigator at a financial institution, and your SIEM flagged unusual activity on a workstation with access to sensitive financial data. Suspecting a breach, you received a memory dump from the compromised machine. Your task is to analyze the memory for signs of compromise, trace the anomaly's origin, and assess its scope to contain the incident effectively.

### Q1 Identifying the name of the malicious process helps in understanding the nature of the attack. What is the name of the malicious process?
To check all suspicious running processes at the time of the memory capture
### Command:
Python vol.py -f <path_of_Memory_dump> windows.malfind
<img width="1919" height="926" alt="Screenshot 2025-11-06 113324" src="https://github.com/user-attachments/assets/e2e0a91e-4864-45b8-abd6-1a619e34c71f" />
### Answer: powershell.exe

### Q2 Knowing the parent process ID (PPID) of the malicious process aids in tracing the process hierarchy and understanding the attack flow. What is the parent PID of the malicious process?
Tracing the origin of the malicious process helps us understand how it was executed:
### Command
Python vol.py -f <path_of_Memory_dump> windows.pstree | grep "PID"
<img width="1919" height="918" alt="Screenshot 2025-11-06 113741" src="https://github.com/user-attachments/assets/3c6d43d3-a072-4b01-9a69-de70cc15e284" />
### Answer: 4120

### Q3 Determining the file name used by the malware for executing the second-stage payload is crucial for identifying subsequent malicious activities. What is the file name that the malware uses to execute the second-stage payload?
For this i used pstree to list the process and grep to filer powershell.exe only 
### Command
Python vol.py -f <path_of_Memory_dump> windows.pstree | grep powershell.exe
<img width="1918" height="920" alt="Screenshot 2025-11-06 113950" src="https://github.com/user-attachments/assets/38469c20-ba93-44dd-a479-e44412445721" />
### Answer: 3435.dll

### Q4 Identifying the shared directory on the remote server helps trace the resources targeted by the attacker. What is the name of the shared directory being accessed on the remote server?
From the precious answer we got pid 3692 and use it as a filter 
### Command 
Python vol.py -f <path_of_Memory_dump> windows.cmdline -pid 3692 
### Answer: davwwwroot

### Q5 What is the MITRE ATT&CK sub-technique ID that describes the execution of a second-stage payload using a Windows utility to run the malicious file?
Using MITRE ATT&CK, we identify the sub-technique used:
The attacker used rundll32.exe to execute a DLL payload, which matches T1218.011.
<img width="975" height="899" alt="1_yWVtODYMhT0fVYOJZfkaAA" src="https://github.com/user-attachments/assets/0cb88c6c-a037-48e8-b640-08225fe2b384" />
### Answer :T1218.011

### Q6 Identifying the username under which the malicious process runs helps in assessing the compromised account and its potential impact. What is the username that the malicious process runs under?
### Command:
python vol.py -f memory.dmp windows.userassist
- Used to identify programs executed by the user
- Helps track user activity and possible attacker actions
<img width="1919" height="920" alt="Screenshot 2025-11-06 114630" src="https://github.com/user-attachments/assets/f8cbb182-382c-4af8-a7d5-938d38be0127" />
### Answer: Elon

### Q7 Knowing the name of the malware family is essential for correlating the attack with known threats and developing appropriate defenses. What is the name of the malware family?
<img width="1919" height="871" alt="Screenshot 2025-11-06 114751" src="https://github.com/user-attachments/assets/2846f7ce-7c66-4ead-89ef-431c4e2fa762" />
- The file is identified as STRELASTEALER, a known malware family.
### Answer: STRELASTEALER
