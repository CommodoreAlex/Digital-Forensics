**Learning Objectives of the Hack The Box Challenge: Forela**

In the **Forela** challenge, participants are tasked with analyzing a compromised Domain Controller (DC) under attack. The primary goal is to perform quick triage and identify any signs of the attacker’s actions. Key objectives of this challenge include:

1. **Understanding Domain Controller Attacks**: Gain insight into the methods used by attackers to compromise a DC, particularly through tools like `vssadmin`, which can be exploited to dump the NTDS.dit database containing sensitive domain data (password hashes, user information, etc.).
    
2. **Analyzing Logs and Artifacts**: Analyze logs and other artifacts provided as part of the challenge to identify suspicious activity. This includes understanding the use of **LOLBINs (Living off the Land Binaries)**, which are legitimate system tools abused by attackers for malicious purposes.
    
3. **Responding to an Attack**: Learn how to conduct initial triage to assess the situation and determine whether the attacker has successfully dumped the NTDS.dit database. This involves detecting the use of `vssadmin` or other suspicious activity indicative of an ongoing attack.
    
4. **Kicking the Attacker**: In addition to triage, participants are challenged to take steps to remove the attacker from the environment if possible. This could include identifying and terminating malicious processes or taking action to secure the DC.

By completing this challenge, learners will improve their skills in **digital forensics**, **incident response**, and understanding common attack vectors in a Windows domain environment.

You can find my detailed solution for this challenge here: [HTB Sherlock: Crown Jewel - Solution](https://www.cyberwiredtraining.net/digital-forensics/htb-sherlock-crownjewel-1).
