# spr330_assignment2
This repo contains the list of attacks I chose to show off for assignment #2 of SPR330. The attacks I will be going over use programs such as mimikatz, bluespawn and metasploit. 

# Attack #1: dcsync_ntlm w/ mimikatz or kiwi
I have included a written summarization as well as a YouTube video explaining how to setup the environment for this attack. DCSync attack is done either through a reverse shell connection or obtains credentials and logs on as the user on a workstation. For the purpose of the attack, I have decided simulate a Reverse TCP connection creating a meterpreter session with the attacker and the workstation using msfvenom and msfconsole. 

## What is a DCSync attack?
The DCSync is an attack that allows the attacker to simulate/replicate actions that normally the Domain Controller (DC) would do in order to retrieve password data of all users in the domain. The attacker for this attack would to compromise an account with Domain Administrator privileges in order to mimic the domain controller. DCSync actions can be found in Mimikatz/Kiwi as the command "Mimikatz" followed by the domain and the user you want to look for. 

### What is required?
You need to set up the current environment:
- 1x Windows Server 2016/2019 with Active Directory configured
- 1x Windows 10 VM 
- 1x Kali Linux VM 


### Step 1. Create a reverse shell session via Meterpreter
With the credit of the BHIS videos I utilized the TrustMe.exe malware that we created in the labs in order to create a reverse_tcp connection. In order to get access to administrator level commands on our shell we had to execute the .exe as an administrator. In the Kali VM I have setup the exploit for a reverse_tcp meterpreter shell through msfconsole. (Check Video for Commands)  For the purpose of the lab I just right clicked on the .exe and ran as an administrator. If we go back to the Kali VM we can see that a meterpreter session was started. 

### Step 2. Setup 

