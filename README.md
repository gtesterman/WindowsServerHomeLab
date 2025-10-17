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
<p align="center">

<p/>
