# spr330_assignment2
This repo contains the list of attacks I chose to show off for assignment #2 of SPR330. The attacks I will be going over use programs such as mimikatz, bluespawn and metasploit. 


# CHANGELOG 12/3/2020
- REPO CREATED

# Attack #1: dcsync_ntlm w/ mimikatz or kiwi
I have included written instructions as well as a YouTube video explaining how to setup the environment for this attack. Originally I wanted to do this in an Active Directory but due to my current knowledge on properly setting up an Active Directory and presenting my knowledge on the attack tool. I decided it would be easier to show it off in a single machine that is isolated. 

### Background Information:
There is a small domain called ajalcantara.com. You have a built-in administrator on the Domain Controller plus three users. Bob, John and Alice. I don't mean to be sexist with the fact that there are more guys it's just what came into my mind as fake users. Anyways, Bob is the domain admin and he just configured John to be the local admin on a workstation in order to maintain the web server from that workstation only. John attempts to download what he thinks is a client to open up the web page editor but instead is hit with a reverse shell given to an attacker. The attacker will then use mimikatz or kiwi to run dcsync and grab all the hashes on the domain. 

#### What is required?
You need to set up the current environment:
- 1x Windows Server 2016/2019 with Active Directory configured
- 1x Windows 10 VM 
- 1x Kali Linux VM 


