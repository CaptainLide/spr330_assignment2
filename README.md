# spr330_assignment2 (Part A)
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

#### Step 1. Create a reverse shell session via Meterpreter
With the credit of the BHIS videos I utilized the TrustMe.exe malware that we created in the labs in order to create a reverse_tcp connection. In order to get access to administrator level commands on our shell we had to execute the .exe as an administrator. In the Kali VM I have setup the exploit for a reverse_tcp meterpreter shell through msfconsole. (Check Video for Commands)  For the purpose of the lab I just right clicked on the .exe and ran as an administrator. If we go back to the Kali VM we can see that a meterpreter session was started. 

#### Step 2. Load Modules in Meterpreter 
When you obtain a meterpreter the kiwi module has not loaded by default. This means that we need to load it manually. Luckilly meterpreter has made it simple to load modules like kiwi and many others. To load kiwi its as simple as typing the command "load kiwi" you will then be greeted with a welcome prompt to loading kiwi which looks like a kiwi. 

#### Step 3. Run DCSync attack!!! 
Final step is crucial, this is where the attack happens. If configured correctly you should be able to run the DCSync commands which are DCSync and DCSync_NTLM. The difference between these two commands is that DCSync gives all information about the user's credentials which we will go over in a later attack and DCSync_NTLM will only show you NTLM hashes of the user you choose to look for.

### Why would you want to run this type of attack? 
There are many reasons why an attacker would want to do this stage of attack despite already having Domain Administrator access. Well the thing is DCSync is a late-stage attack meaning this is usually done after the attacker has successfully found a hole in the network. One reason why an attacker would want to do this is because they may need a specific user's credentials that will access certain files or simply to gather information about the domain. Attackers don't just look for passwords.  

# Attack #2: PtH Attack 
PtH stands for Pass-The-Hash and is a common method used to achieve lateral movement within a domain. Since MFA is slowly being implemented across many organizations especially due to the COVID-19 Pandemic that has lead to many people working-from-home since March its become crucial that many employees add MFA in order to login to their network over a VPN. PtH makes it possible to move laterally across a network without MFA which is why this type of attack is especially dangerous. 

### What is required?
Pretty much the same as Attack #1:
- 1x Windows Server 2016/2019 with Active Directory configured
- 1x Windows 10 VM 
- 1x Kali Linux VM  

#### Step 2. Load Mimikatz 
Since we are going to gain information using the DCSync command we're going to need to load up the Mimikatz application installed on John Doe's account.

#### Step 3. Let's choose a user to gain access to. 
Currently my user 'John Doe' is the one I am logged into. Let's see if we can go to Alice's account even if she is a Domain User with no Administrator privileges. To do that we will run another DCSync attack and find the AES256 Hash tied to her account. 

#### Step 4. PtH Attack!!!
In Mimikatz there is a command called "sekurlsa" followed by two colons with the word "pth". We will then choose the user, their domain and the aes256 hash tied to it that we found via DCsync. 

# Attack #3: Password Dump with Mimikatz
Not all attacks have to be done by compromising the Active Directory, some attacks only require to compromise one sole machine. This attack will also show off why its crucial that organizations update their endpoints as much as possible because exploits are being produced everyday. 

### What is required?
- Windows 7 VM (Mimikatz dumps plaintext passwords in Windows 7) 

#### Step 1. Install Mimikatz
Mimikatz can be downloaded in a github link. https://github.com/gentilkiwi/mimikatz make sure to extract the directory somewhere where it can be easily accessed for the lab. 

#### Step 2. Load Mimikatz 
Mimikatz is an executable found in the x64 subfolder of the Mimikatz folder extracted. We will need to escalate privileges so make sure to run it as an administrator. 

#### Step 3. Escalate Privileges
Escalating privileges is pretty easy in Mimikatz. If executed properly you can type the command "privilege::debug". You should now be able to run the next command which will dump all passwords. 

#### Step 4. Dump Passwords!!! 
In order to dump passwords we will need to sue the command ```sekurlsa::logonpasswords Full``` which will dump all contents about the user's passwords that are saved to memory. Optionally you can keep this in a log file in order to have a text file for reference. 



























