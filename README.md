# AzureHoneypot Building a SOC + Honeypot in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/c600ecd6-b927-4032-b41d-0e2c821f29d5)


## Introduction

In this project, I build a honeypot in Azure, ingest log sources and integrate them into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents based on the ingested logs. The final product is a map of the attackers attempts to gain entry into the system.



## Creation / Configuring of Virtual Machine and Log Analytics Workspace

Here we are Microsoft Azure creating our Virtual Machine, making sure to allow traffic for all ports. This is done in order to be as discoverable as possible.
![Architecture Diagram](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/4a87d7e0-a1e7-43a7-8dfb-eeb84bc12f75)

After creating the VM, a new Log Analytics Workspace (LAW) needs to be created in Azure. 
![Architecture Diagram](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/8c3061c0-9036-4b87-b86d-3c4d270e3b4b)

Connecting VM 

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/1f7f0a5e-45ff-4ed6-b002-24cef24be1d1)


## Logging into Remote Desktop / LAW Advanced configuration

![Architecture Diagram](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/10ca4029-1084-4813-947e-efd1ac1f5d9a)

The above image depicts logging into VM using Remote Desktop Connection. Once inside the VM, the firewall rules need to be turned off, and a ping request can be initiated from the user system to the Virtuals Machine's IP, just to double check that it is discoverable. From there, we take our PowerShell script and go into PowerShell ISE and use the script to create our failed.rdp file and give us entries to use to help the LAW and Sentinel properly map our information.

This image below is an example of the the Powershell script running in the Log Analytics Workspace to properly display our test entries of bad actors displaying information about them including IP address, latitude, longitude, city, state, date, time etc. These will also be able to be viewed after for further review if necessary.

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/9babbbd3-ed9a-4a67-bbf6-dbaa5996d4e0)


## Sentinel Integration 

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/6b9fd331-e3fb-4f4a-93ff-1d81d76ca4b0)

Opening and configuring Sentinel is an essential part of the project as it allows for the points to be plotted on the world map for information that is easier to visualize and understand

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/d8242f8c-16c9-4121-905f-0fdad58b0d1b)

Here we are running the script in our new workbook and configuring the map settings. You will also see in the image below, that within the Remote Desktop, the script in PowerShell is still running allowing us to continually collect data that is then used to plot the points on the map. 

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/b254d12e-5f5b-4f06-8b37-4aba294a84e7)

In this particular instance, the username is seen as “failingtotest”. This was done by myself just to be sure everything was working correctly, because about 10 minutes had gone by without any entries. The script is running, and it didn’t take long for threats to discover the machine and attack.


## Attack Map Visualization

Within minutes there were 2 attempts from Panama, and 92 from Saudi Arabia. The 1 from the United States is the "failingtotest" entry done purposely prior.

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/2d76fb87-da68-4657-8e62-b3ba16be604e)

Only about 10 minutes later and the attacks from Saudi Arabia grew from 92 to 421 attempts.

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/666f8cac-b2f3-4d80-b83b-f604e153fb5f)

About 20 more minutes and over one THOUSAND attempts'

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/73324b5c-f67b-4e13-915d-5fa689ce26af)

Here, in the image below, we can see the plots being displayed more clearly. Saudi Arabia has over 3 thousand attempts and growing steadily. All of this happened in a matter of minutes. Imagine the impact this could have on an actual machine with personal information, such as credit card data, company secrets, or even things such as SSN’s or PII. The sheer volume and persistence of these attempts highlight the critical need for robust cybersecurity measures. The implications extend beyond data breaches to the compromise of personal and financial security, emphasizing the urgency for organizations to fortify their defenses against threats. 

![image](https://github.com/Scottiesene/AzureHoneypot/assets/151565915/75f21bc0-4826-4f7c-9030-07a7ad26e180)



## Conclusion

In this project, a honeypot was constructed in Microsoft Azure and log sources were integrated into a Log Analytics Workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. The decision to undertake and craft this project was inspired by the goal to showcase skills and experience utilizing Microsoft Azure amongst other technologies, with a deliberate focus on presenting evidence of the consequences that can occur, while also teaching a valuable lesson pertaining to hardening your devices and lessening your attack surface. Making sure to keep firewalls and security configurations up to date is something minimal we can do to protect digital ecosystems against malicious activities.   

It is worth noting that if the project is redone, the entries will always be different. There are always bad actors from around the world attempting to break into unprotected machines. The longer the script is allowed to run in this environment, the more entries will occur from different places. For this reason, no implementation of this project is exactly the same.
