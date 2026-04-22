### Scenario
You are a cybersecurity analyst working in the Security Operations Center (SOC) of BookWorld, an expansive online bookstore renowned for its vast selection of literature. BookWorld prides itself on providing a seamless and secure shopping experience for book enthusiasts around the globe. Recently, you've been tasked with reinforcing the company's cybersecurity posture, monitoring network traffic, and ensuring that the digital environment remains safe from threats.
Late one evening, an automated alert is triggered by an unusual spike in database queries and server resource usage, indicating potential malicious activity. This anomaly raises concerns about the integrity of BookWorld's customer data and internal systems, prompting an immediate and thorough investigation.
As the lead analyst in this case, you are required to analyze the network traffic to uncover the nature of the suspicious activity. Your objectives include identifying the attack vector, assessing the scope of any potential data breach, and determining if the attacker gained further access to BookWorld's internal systems.

### Q1 By knowing the attacker's IP, we can analyze all logs and actions related to that IP and determine the extent of the attack, the duration of the attack, and the techniques used. Can you provide the attacker's IP?
Used Wireshark display filters and navigated to Statistics → Endpoints → IPv4 to analyze network endpoints.
<img width="1920" height="1080" alt="Screenshot (309)" src="https://github.com/user-attachments/assets/016ae05d-92cc-47d3-9160-fa0783f54b3a" />
### Answer: 111.224.250.131

### Q2 If the geographical origin of an IP address is known to be from a region that has no business or expected traffic with our network, this can be an indicator of a targeted attack. Can you determine the origin city of the attacker?
Search the ip address in whois lookup
<img width="1920" height="1080" alt="Screenshot (310)" src="https://github.com/user-attachments/assets/c6b7ba17-db6c-4737-ac18-a3b8e3b10247" />
### Answer: Shijiazhuang

### Q3 Identifying the exploited script allows security teams to understand exactly which vulnerability was used in the attack. This knowledge is critical for finding the appropriate patch or workaround to close the security gap and prevent future exploitation. Can you provide the vulnerable PHP script name?
To determine the exploited PHP script, HTTP requests were filtered in Wireshark.
http.request.uri.path == "/search.php"
This filter was used to narrow down traffic specifically to /search.php, helping identify whether this script was accessed or exploited by the attacker.
<img width="1920" height="1080" alt="Screenshot (311)" src="https://github.com/user-attachments/assets/7ac0dab6-dda3-448f-be83-bbac9f1cd5ee" />

### Q4 Establishing the timeline of an attack, starting from the initial exploitation attempt, what is the complete request URI of the first SQLi attempt by the attacker?
For this open the packet and analyze the request and decode that string 
<img width="1920" height="1080" alt="Screenshot (314)" src="https://github.com/user-attachments/assets/b0ea7a10-b308-4dd3-8a81-cd698f3c566b" />
### Answer: /search.php?search=book and 1=1; -- -

### Q5 Can you provide the complete request URI that was used to read the web server's available databases?
so SCHEMATA is a system table used to list all databases, commonly targeted during SQL injection for enumeration.
So I searched http.contains "SCHEMATA" string, then finally obtained the answer
<img width="1920" height="1080" alt="Screenshot (315)" src="https://github.com/user-attachments/assets/adcd90b3-a175-44a4-adf2-17adc36b7371" />
### Answer: /search.php?search=book' UNION ALL SELECT NULL,CONCAT(0x7178766271,JSON_ARRAYAGG(CONCAT_WS(0x7a76676a636b,schema_name)),0x7176706a71) FROM INFORMATION_SCHEMA.SCHEMATA-- -

### Q6 Assessing the impact of the breach and data access is crucial, including the potential harm to the organization's reputation. What's the table name containing the website users data?
<img width="1920" height="1080" alt="Screenshot (319)" src="https://github.com/user-attachments/assets/cdad0b39-41eb-4b4d-8548-5dcfb61eb139" />

### Answer: customers

### Q7 The website directories hidden from the public could serve as an unauthorized access point or contain sensitive functionalities not intended for public access. Can you provide the name of the directory discovered by the attacker?
<img width="1920" height="1080" alt="Screenshot (320)" src="https://github.com/user-attachments/assets/af07fa80-4d98-4c14-8026-4bca3a2d8c0f" />
### Answer: /admin/

### Q8 Knowing which credentials were used allows us to determine the extent of account compromise. What are the credentials used by the attacker for logging in?
### Answer: admin:admin123!

### Q9 We need to determine if the attacker gained further access or control of our web server. What's the name of the malicious script uploaded by the attacker?
<img width="1920" height="1080" alt="Screenshot (320)" src="https://github.com/user-attachments/assets/86995795-5a06-453e-8d90-2503fbd596e1" />
### Answer: NVri2vhp.php
