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


