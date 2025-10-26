<h1>Windows Home Lab with Active Directory</h1>
<h2>Description</h2>
This project consists of a virtual Windows environment with Active Directory users connected to the domain. The environment was created in VMware Workstation Pro by connecting virtual machines through an internal network adapter and using Active Directory to attach the clients to the internal domain. The VMs consist of Windows Server 2025 for the domain controller and DHCP Server, with Windows 11 Enterprise deployed as the client. The purpose of this set up is to have an educational lab environment ready for vulnerability analysis and exploitation.
<br />
I based this project on Josh Madakor's walkthrough for a home lab. His video uses older VMs but I will be utilizing the same basic architecture. If you are interested in watching the original lab you may do so

[here](https://www.youtube.com/watch?v=MHsI8hJmggI&list=PLyiUopSz5rksEMcTUVJUFvoWMp00rGH31&index=4).
<br />
<h2>Applications Used</h2>

- <b>[Vmware Workstation Pro](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)</b>
- <b>PowerShell</b>
<h2>Environments Used </h2>

- <b>[Windows Server 2025](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2025?msockid=3653bc85d863632634beaa02d91a62b3)</b>
- <b>[Windows 11](https://www.microsoft.com/en-in/evalcenter/download-windows-11-enterprise)</b>

<h2>Hardware Requirements </h2>

- <b>16GB RAM</b>
- <b>124GB Storage</b>
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
  - Create a username and password for the machine <br />
  - Product key is not needed if you are using the free trial from Microsoft Evaluation Center <br />
⚠️IMPORTANT: If you don't set up a password now, you will be unable to create a domain
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
- Promote the server to a domain controller in Server Manager
<br />
<p align="center">
<img width="448" height="488" alt="Screenshot 2025-10-21 121715" src="https://github.com/user-attachments/assets/94be0759-8dd0-4321-b803-180755f99cb4" />
<p/>
<br />
<br />
- Add a new forest and create a domain name
<br />
<p align="center">
<img width="757" height="606" alt="image" src="https://github.com/user-attachments/assets/951d13bf-bcfd-4d24-8e63-b72d25765222" />
<p/>
<br />
<br />
- Create a Directory Services Restore Mode password <br />
- Keep everything else default and install Active Directory Domain Services
<br />
<p align="center">
<img width="860" height="622" alt="image" src="https://github.com/user-attachments/assets/05c42657-c114-4f84-96b8-d361d6bf4498" />
<p/> 
<br />
<br />
Use Active Directory Users and Computers to create your admin account: <br />
- Place the admin account in an Organizational Unit for administrators <br />
- Add the admin account to the "Domain Admins" user group <br />
- (optional) Use a PowerShell script to add your domain users to an Organizational Unit.
<br />
<p align="center">
  <img width="1167" height="986" alt="Screenshot 2025-10-21 185131" src="https://github.com/user-attachments/assets/3bc7d75c-0ab7-4024-9624-db8b0242e249" />
<img width="777" height="555" alt="Screenshot 2025-10-19 171337" src="https://github.com/user-attachments/assets/d66d6075-e55b-41b7-af88-116c301669d7" />
<p/>
<br />
<br />
Use the "Add Roles and Features" wizard to add Remote Access to the server. <br />
  - This will allow NAT for the client computers in your local network.
<br />
<p align="center">
<img width="830" height="664" alt="image" src="https://github.com/user-attachments/assets/36feef46-bfb8-4413-97d1-e0644d31eeab" />

<img width="801" height="641" alt="image" src="https://github.com/user-attachments/assets/5620b781-d7cf-4d25-b404-a37894424f42" />

<img width="853" height="683" alt="image" src="https://github.com/user-attachments/assets/dc49b39f-c5b3-49b9-8d68-9c14eba251d2" />

<p/>
<br />
<br />
- Use the Routing and Remote Access tool to add NAT for your internet-facing network
<br />
<p align="center">
<img width="433" height="879" alt="Screenshot 2025-10-21 191203" src="https://github.com/user-attachments/assets/7dbc06ca-8530-4cf2-bd68-2619ba9249c0" />

<img width="793" height="524" alt="Screenshot 2025-10-21 191255" src="https://github.com/user-attachments/assets/1192d034-ff84-4ea4-9d5a-792e3a50338d" />

<img width="659" height="472" alt="Screenshot 2025-10-21 191339" src="https://github.com/user-attachments/assets/6b08a6eb-694d-407d-8779-300d7d93b84c" />

<img width="764" height="515" alt="Screenshot 2025-10-21 191847" src="https://github.com/user-attachments/assets/181911a9-b13f-43cf-8c50-5e4b21b24336" />

<img width="789" height="536" alt="Screenshot 2025-10-21 191942" src="https://github.com/user-attachments/assets/2c8ae7f0-f857-40f3-8cc4-51c90760347c" />

<p/>
<br />
<br />
- Open Server Manager > Tools > DHCP <br />
- Set up your DHCP Server with the network details used in the internal network <br />
Address Range = 172.16.0.100 - 172.16.0.200 <br />
Subnet Mask = 255.255.255.0 
<br />
<p align="center">
<img width="1011" height="895" alt="Screenshot 2025-10-21 192338" src="https://github.com/user-attachments/assets/049fd305-6290-4474-aa39-bfbfc47a16f4" />
<p/>
<br />
<br />
- Use the domain controller ip for the default router and DNS servers
<br />
<p align="center">
<img width="1025" height="846" alt="Screenshot 2025-10-21 192511" src="https://github.com/user-attachments/assets/478da250-6112-4212-a407-ba52e3dd7270" />

<img width="1010" height="871" alt="Screenshot 2025-10-21 192534" src="https://github.com/user-attachments/assets/0f06bd73-bc9a-4171-b7fb-e9d7a164d92c" />
<p/>
⚠️IMPORTANT: In order for the server to work you will need to refresh DHCP by right-clicking on the IPv4 server.


<br />
<br />

<br />
<p align="center">

<p/>
  
<br />
<br />
Create the Workstation VM:<br />
- Create a new machine with the windows 11 ISO <br />
- Use default settings and host-only network adapter <br />
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
- Computer will welcome you and prompt for credentials then force a restart
<br />
<p align="center">
<img width="825" height="660" alt="image" src="https://github.com/user-attachments/assets/524445d1-ae99-4aa7-9ad5-f9f5e9c00225" />

<img width="815" height="652" alt="image" src="https://github.com/user-attachments/assets/2c550696-82cf-4b60-9bd8-6713f728e88f" />

<img width="767" height="613" alt="image" src="https://github.com/user-attachments/assets/82af441a-a6a4-4493-9180-dd491c7718c8" />

<p/>
<br />
<br />
- Once restarted, the workstation should be able to log in with domain credentials.
<br />
<p align="center">
<img width="1032" height="826" alt="image" src="https://github.com/user-attachments/assets/bed668b2-5223-46be-b87b-02c6fa4eeba6" />

<p/>
<br />
<br />
- To manage domain computers, use the Computers folder in Active Directory
<br />
<p align="center">
<img width="842" height="674" alt="image" src="https://github.com/user-attachments/assets/d275ba75-6791-43d0-a2f6-f84137257e28" />

<p/>
<br />
<br />
<b> Once the client is connected to the domain and has a working Internet connection through the DHCP server, the Windows home lab setup is complete.</b>
