## Scenario
As a member of the Security Blue team, your assignment is to analyze a memory dump using Redline and Volatility tools. Your goal is to trace the steps taken by the attacker on the compromised machine and determine how they managed to bypass the Network Intrusion Detection System (NIDS). Your investigation will identify the specific malware family employed in the attack and its characteristics. Additionally, your task is to identify and mitigate any traces or footprints left by the attacker.

# Q1 What is the name of the suspicious process?
To detect potentially malicious processes, the `malfind` plugin in Volatility was used. This plugin scans memory for injected code and suspicious regions.

### Command Used
vol.py -f “/path/to/file” windows.malfind
<img width="1918" height="883" alt="Screenshot 2025-11-07 163512" src="https://github.com/user-attachments/assets/da1f5599-de14-454c-9470-9b8b08903fcc" />
after it using it’s scanning part you can find the process oneetx.exe in here with process ID 5896
# Answer: oneetx.exe

# Q2 What is the child process name of the suspicious process?
Now after we knew the suspicious process and it’s PID now we need to check what child process it has spawned. we can do this through searching processes list with process ID 5896 to spot any processes associated with it.

### Command Used
python vol.py -f "/path/to/file" windows.pslist | grep 5896
<img width="1919" height="921" alt="Screenshot 2025-11-07 163938" src="https://github.com/user-attachments/assets/f41bd65c-43f5-4457-9522-a7ec6b83f2a7" />
# Answer: rundll32.exe

# Q3 What is the memory protection applied to the suspicious process memory region?

### Command:
vol.py -f memory.dmp windows.malfind

- Found memory protection: **PAGE_EXECUTE_READWRITE**
- This is suspicious because it allows both writing and executing code in memory.
# Answer:PAGE_EXECUTE_READWRITE

# Q4 What is the name of the process responsible for the VPN connection?

 we need to check the connections in our memory dump. to check if we can spot any suspicious outbound connection to suspicious IP or port.

which you can do through the commands to review them:

### Command:
- vol.py -f “/path/to/file” windows.netscan
- vol.py -f “/path/to/file” windows.netstat
- 
we can find 2 intersting connections as follows:
- connection towards 77.91.124.20 on port 80 done by oneetx.exe which is our confirmed malicious process
- connection towards 38.121.43.65 on port 443 by tun2socks.exe for which IP is not for microsoft and the process name for it is not fimiliar.

<img width="1919" height="920" alt="Screenshot 2025-11-07 164255" src="https://github.com/user-attachments/assets/e0a9eef7-b904-4719-8cec-f6d24f475179" />
<img width="1918" height="923" alt="Screenshot 2025-11-07 164038" src="https://github.com/user-attachments/assets/1a352013-6441-49bd-9cf4-1f6c93643d0b" />

we find here that it’s PID is 4628 we can find it using our pslist | grep 4628 to check who is the parent
we find the parent process ID for tun2sock.exe is 6724 which we will look for it in the process lists
and yes we can find it and it is Outline.exe
# Answer: Outline.exe

# Q5 What is the attacker's IP address?

we find oneetx.exe has connection to 77.91.124.20 on port 80. which means this is probably the attacker’s IP.
<img width="1919" height="950" alt="Screenshot 2025-11-07 164750" src="https://github.com/user-attachments/assets/eba3c60f-58b2-4e0e-a0eb-a2f341aa2b7c" />

# Q6 What is the full URL of the PHP file that the attacker visited?
i used grep command to search and filter 
### Command:
strings MemoryDump.mem | grep 77.91.124.20
<img width="1919" height="923" alt="Screenshot 2025-11-07 170426" src="https://github.com/user-attachments/assets/48a80f01-9a38-4eaf-b3ce-998340ede70b" />
# Answer : http://77.91.124.20/store/games/index.php

# Q7 What is the full path of the malicious executable?
we know the malicious process name and it’s ID we can grap this info using pstree:
### Command:
python vol.py -f ‘path/to/file’ windows.pstree — pid 5896
<img width="1917" height="924" alt="Screenshot 2025-11-07 170531" src="https://github.com/user-attachments/assets/d014fd37-fa7b-4bde-8f61-c9b0186f51bf" />

