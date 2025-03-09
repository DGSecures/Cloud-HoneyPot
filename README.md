# Azure Honeypot Lab 

## Objective 

The Azure Honeypot Lab project is aimed to establish a cloud enviornment with a deliberately vulnerable machine. The setup is designed to attract real-time, authentic cyber attacks, allowing the capture of detailed logs of attacker behavior. The primary focus was collect genuine attack data that could be analyzed to expose cyber criminal Tactics, Techniques, and Procedures (TTPs). This hands-on experience was designed to deepen an understanding of attack patterns and strengthening exposure to cloud environment and their resources. 

### Skills Learned

- Provisioned and configured a virtual machine (VM) in an Azure environment.
- Developed proficiency in VM log extraction and analysis.
- Development understaning of Microsoft Sentinel.
- Proficiency in analyzing and interpreting Event Viewer logs.
- Exposure to Windows Firewall personalization 

### Tools Used

- Azure Virtual Machines
- Azure Virtual Networks
- Microsoft Sentinel
- Log Analytics Workspaces
- RDP

### Environments Used

 - Microsoft Azure
 - Windows 10 Pro

  ### Program Walk-Through
  
<p align="center">
  Azure Portal Landing Page with Resources Utilized.
</p>

![Screenshot 2025-03-04 184757](https://github.com/user-attachments/assets/2d39b87c-30c6-4546-9ad7-7f1841e2950a)

<p align="center">
  Next we create a Virtual Network with a private IP address that our VM will use later on. Virtual Networks create a subnet that can be utilized. 
</p>

![Screenshot 2025-03-05 201818](https://github.com/user-attachments/assets/dc308fb8-ee1b-4792-9334-909718bc5817)

<p align="center">
  We then setup our VM within Azure connecting it to our Virtual Network Previously created.
  It is assigned an IP within the Virtual Network along with a public IP (This is important later)
  We are able to use RDP to remote into our VM using its public IP address.
</p>

![Screenshot 2025-03-03 185429](https://github.com/user-attachments/assets/402a66cb-b083-4de7-88c8-86b1bc49506e)

<p align ="center">
Once connected to our VM in the cloud, we navigate to its firewall settings and we are going to esentially make it open by turning off the firewall states for each profile.
</p>

![Screenshot 2025-03-03 185851](https://github.com/user-attachments/assets/714950eb-69e4-4903-816c-b1d59c304d23)

<p align ="center">
We can now go on our local machine and see that our VM is reachable over the internet by pinging it.
</p>

![ping](https://github.com/user-attachments/assets/de8a4353-0a81-403c-b476-8c0c42bd3e00)

<p align ="center">
We'll now concentrate on the brute-force attacks we'll be observing, which are attempts to log in to our VM. The following screenshots show how failed login attempts appear in Event Viewer. We'll be collecting and displaying these events at the end. We went ahead and tried to RDP into the VM using incorrect credentials to generate the logs. The first screenshot displays how the event looks logged. The second screenshot gives us more information on one of the logs such as the name of the workstation attempting to connect + the source network address. 
</p>

![Screenshot 2025-03-03 190629](https://github.com/user-attachments/assets/19a7154d-9602-4880-9e9d-0bee242c59d0)
![Screenshot 2025-03-03 190707](https://github.com/user-attachments/assets/030fa7f9-4f6f-4461-9890-e8bbb799f0b6)

<p align ="center">
After we have seen what a failed login attempt looks like, we then want to be able to see these attempts outside of the VM. This is where we create what is known as a Log Analytics workspace. In short, this collects log data from our Azure resources such as our VM. 
</p>

<p align ="center">
Once we have created our Log Analytics Workspace, we want a way to be able to actually access those logs. We do this by creating our Microsoft Sentinel instance which is a cloud-native SIEM and adding our newly created Log Analytics Workspace to Sentinel.  
</p>

![Screenshot 2025-03-09 140756](https://github.com/user-attachments/assets/e4650501-55e1-4d56-8ea6-dcaba05ec8d4)

<p align ="center">
We will now configure Windows Security Events in Microsoft Sentinel, using the Azure Monitor Agent (AMA), to ingest security event logs from our VM into our Log Analytics Workspace. This AMA configuration is the core component that streams our VM events into Microsoft Sentinel, which we will then use to display the information.
</p>

![Screenshot 2025-03-03 192000](https://github.com/user-attachments/assets/9a315c59-a381-4a8c-b2a6-d9d4d329cd4f)

<p aligh="center">
Once we have installed our Azure Monitoring Agent, we then want to configure it. We will create a data collection rule within AMA to inform our VM to actually forward the logs.
</p> 

![Screenshot 2025-03-03 192212](https://github.com/user-attachments/assets/9f47c4d6-3b8b-4126-b35f-27721a6aaeb7)

<p aligh="center">
At this point, all the main configurations have been completed and our VM should be sending over security logs from its Event Viewer. From here, we could go into our Log Analytics Workspace, navigate over to Logs, and create a Security Events query that will filter to display failed login attempts.
</p> 

![Screenshot 2025-03-09 142703](https://github.com/user-attachments/assets/266cd91a-c1f1-4798-9dda-89115b37aa03)

<p aligh="center">
From the screenshot above, we see the account name the attacker was attempting to use along with the date and time. You also see EventID 4625 which is the ID associated with a failed audit in Windows Event Viewer. To give us a better understanding of where the attacks our coming from, we have imported a sheet that lists out ranges of networks and their associated countires into a Watchlist in Microsoft Sentinel.  
</p>

<p aligh="center">
We will now utilize the Workbooks feature in Microsoft Sentinel to display the attacks on a map. In the Workbook, we also run a query from a created Watchlist that will display the information we previously saw in the logs of our Log Analytics Workspace. The map represents the attack volume with different sized circles. Larger circles indicate a higher volume of attacks from that location.   
</p>

<p aligh="center">
This first map was taken a little over 24 hours after we exposed our VM to the internet.
</p>

![Screenshot 2025-03-04 175338](https://github.com/user-attachments/assets/8b6f3513-eef9-4d66-a4aa-e340987201be)

<p aligh="center">
This second map was taken about 6 days after exposing our VM to the internet.
</p>

![Screenshot 2025-03-09 144327](https://github.com/user-attachments/assets/7efdefa8-a1d1-4927-b464-11ce01e0068d)


