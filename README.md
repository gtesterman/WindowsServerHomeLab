<h1>Windows Home Lab with Active Directory</h1>
<h2>Description</h2>
Project consists of a virtual Windows environment with 1000+ users connected to the domain. The environment was created in VMWare Workstation Pro by connecting virtual machines through an internal network adapter and using Active Directory to attach the clients to the internal domain. The VMs consist of Windows Server 2025 for the domain controller and DHCP Server, with Windows 11 Enterprise deployed as the client. The purpose of this set up is to have an educational lab environment ready for vulnerability analysis and exploitation.
<br />
I based this project on Josh Madakor's walkthrough for a home lab. His video is a little bit older but I will be utilizing the same basic architecture. If you are interested in watching the original lab you may do so here.
<br />
<h2>Applications Used</h2>

- <b>Vmware Workstation Pro (for virtualization)</b>
- <b>PowerShell</b>
<h2>Environments Used </h2>

- <b>Windows Server 2025</b>
- <b>Windows 11</b>

<h2>Hardware Requirements </h2>

- <b>16GB RAM</b>
- <b>100GB Storage</b>
<br />
<br />

<h2>Project Walk-Through:</h2>
<b>Download the ISO files<b/> <br/>
<br />
<br />
Create a new virtual machine:  <br />
  - Select the ISO file for the Windows Server
<br/ >
<p align="center">
<img width="428" height="430" alt="Screenshot 2025-10-16 181839" src="https://github.com/user-attachments/assets/1ae3651d-4a47-4211-8c86-6ce04253d12d" />
<p/>
<br />
<br />
  - Create a username and optional password for the machine <br />
  - Product key is not needed if you are using the free trial from Microsoft Evaluation Center
<br />
<p align="center">
<img width="428" height="430" alt="Screenshot 2025-10-16 182946" src="https://github.com/user-attachments/assets/23fb9b92-d905-403b-83e5-66ae17e9dfa1" />
<p/>
<br />
<br />
  - Set up the network adapters <br />
    - Network Adapter 1 = NAT <br />
    - Network Adapter 2 = host only <br />
  - Keep everything else default
<br />
<p align="center">
<img width="428" height="430" alt="Screenshot 2025-10-16 184047" src="https://github.com/user-attachments/assets/52d3b0f4-1dd1-4057-ac76-63b9473b62e3" />
<p/>  
<br />
<br />
  - Launch the VM <br />
  - To unlock the Windows server, send a Ctrl+Alt+Del using VMWare
  <br />
<p align="center">
<img width="752" height="602" alt="Screenshot 2025-10-16 230316" src="https://github.com/user-attachments/assets/3fb291a2-51e1-4431-82f6-329b077ebc68" />
<p/>
<br />
<br />
  - Once unlocked, the VM will prompt you to install VMWare Workstation Tools. This may prompt for a restart.
<br />
<p align="center">
<img width="2560" height="1392" alt="Screenshot 2025-10-16 203042" src="https://github.com/user-attachments/assets/3a38cb88-6e9e-45e9-bee7-12ccec9cece6" />
<p/>
<br />
<br />
Set up the domain controller:  <br />
- Verify the network connections <br />
- Label the internal network adapter and set up IPv4
<br />
<p align="center">
<img width="420" height="469" alt="Screenshot 2025-10-16 231548" src="https://github.com/user-attachments/assets/21cc4fc2-a115-43f8-a473-b19dd71c6255" />
<p/>
<br />
<br />
- Go to Server Manager > Add Roles and Features
<br />
<p align="center">
<img width="1032" height="788" alt="Screenshot 2025-10-16 203619" src="https://github.com/user-attachments/assets/7aef8b5d-c1be-4d34-921d-d180d88c83bb" />
<p/>
<br />
<br />
- Install Active Directory Domain Services, DHCP, and DNS <br />
- Create the domain name for your network <br />
- Restart may be required
<br />
<p align="center">
<img width="798" height="566" alt="Screenshot 2025-10-16 231634" src="https://github.com/user-attachments/assets/e94f405c-d945-4ced-b5b6-b60078750715" />
<p/>
<br />
<br />
- Use Active Directory to create your admin account <br />
- Use Powershell script to add your users to the "Users" Organizational Unit.
- Place the admin account in an Organizational Unit for "Admins"
<br />
<p align="center">
<img width="777" height="555" alt="Screenshot 2025-10-19 171337" src="https://github.com/user-attachments/assets/d66d6075-e55b-41b7-af88-116c301669d7" />
<p/>
<br />
<br />
- Open Server Manager > Tools > DHCP <br />
- Set up your DHCP Server with the network details used in the internal network <br />
Address Range = 172.16.0.100 - 172.16.0.200 <br />
Subnet Mask = 255.255.255.0 
<br />
<br />
<br />
<br />
Create the Workstation VM:<br />
- Create a new machine with the windows 11 ISO <br />
- Use default settings and host-only network adapter
- Launch the VM and start the installation  
<br />
<p align="center">
<img width="1099" height="879" alt="Screenshot 2025-10-04 190933" src="https://github.com/user-attachments/assets/4fd973fc-a0e6-4d21-aef4-041a5e5b0bd1" />
<img width="1051" height="1196" alt="Screenshot 2025-10-04 180354" src="https://github.com/user-attachments/assets/37eabe14-a303-449b-af62-eb912810b4c0" />
<p/>
<br />
<br />
- When getting started with the workstation, select "I don't have Internet" <br />
- Keep all other settings to your preference
<br />
<p align="center">
<img width="1032" height="774" alt="Screenshot 2025-10-04 180133" src="https://github.com/user-attachments/assets/c157f260-a3ec-43b4-adf8-1b9f4ef922b4" />
<p/>
<br />
<br />
- Use Command prompt to confirm you have a connection to the Windows Server <br />
- Go to Settings > System Properties to change your computer's name and make it a member of the domain <br />
- Computer will prompt for crendentials then force a restart
<br />
<p align="center">
<img width="1003" height="802" alt="Screenshot 2025-10-04 223300" src="https://github.com/user-attachments/assets/fb4ca9d4-06e1-4448-8a48-4c486c7121ba" />
<p/>
<br />
<br />
- Once restarted, the workstation should be able to be logged into with domain credentials and have access to the Internet through the DHCP server.
<br />
<p align="center">
<img width="1032" height="985" alt="Screenshot 2025-10-04 225226" src="https://github.com/user-attachments/assets/c8bea4d2-b521-458f-97cd-1a378c1f59af" />
<p/>
<br />
<br />







<br />
<p align="center">

<p/>
<br />
<br />
