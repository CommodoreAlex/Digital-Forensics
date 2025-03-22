# Learning Objectives of the Hack The Box Challenge: CrownJewl-1  

In the **CrownJewl-1** challenge, participants analyze a compromised **Domain Controller (DC)** under attack. The objective is to perform **rapid triage**, identify the attacker's actions, and assess the impact of the breach.  

## Key Objectives  

### Understanding Domain Controller Attacks  
- Learn how attackers compromise **Windows Domain Controllers**, focusing on techniques used to extract sensitive domain data.  
- Investigate **vssadmin abuse** to dump the **NTDS.dit** database, which contains **password hashes** and other critical user information.  

### Analyzing Logs & Artifacts  
- Examine **event logs, process execution data, and system artifacts** to detect **Living off the Land Binaries (LOLBINs)** and other malicious activities.  
- Understand how attackers use **built-in Windows utilities** to evade detection.  

### Incident Response & Attack Mitigation  
- Conduct **initial triage** to determine if the attacker successfully dumped **NTDS.dit** or escalated privileges.  
- Detect and analyze **vssadmin** usage or other suspicious commands indicative of **persistence techniques**.  

### Evicting the Attacker  
- Identify **malicious processes, unauthorized accounts, and backdoors** left by the attacker.  
- Take appropriate steps to **secure the Domain Controller** and remove unauthorized access.  

## Solution Write-Up  
For a detailed step-by-step solution to the **CrownJewl-1** challenge, check out my write-up here: **[HTB Sherlock: Crown Jewel - Solution](https://www.cyberwiredtraining.net/digital-forensics/htb-sherlock-crownjewel-1)**. 

**Challenge Artifacts:** The **CrownJewl1.zip** file, which contains the necessary forensic artifacts, is available in the root of this repository: **[Download Here](CrownJewel1.zip)** and click 'view raw'.
