<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)

<h2>List of Prerequisites</h2>

- Microsoft Azure (Virtual Machine)
- osTicket Installation Files


<h2>Installation Steps</h2>

<p>First things first, we need to create a VM inside Azure. Start by creating a resource group (you can actually create one while setting up the VM). Create a name for the VM, I called mine osticket-vm. Then pick the region; I chose Canada Central since it's the closest for me. For the image, I went with Windows 10 Pro, version 22H2 - x64 Gen2. That should be good enough for this project. </p>

<img width="800" alt="Screenshot 2025-06-17 at 11 20 08 AM" src="https://github.com/user-attachments/assets/659bd8b4-8c6d-49fb-a3e9-20d236ca584b" />


<p>Next, scroll down to select the VM size. I went with Standard_D2s_v3 — 2 vCPUs and 8 GiB of memory. This is more than enough for what we’re doing, but feel free to pick a bigger size if you need more power later. 

Also, I went ahead and made a username and password for the VM — I’ll be using that to log in later. Don’t forget to check the little box for the licensing, and then just hit Review + Create to finish it up.
</p>

<img width="800" alt="Screenshot 2025-06-17 at 12 02 39 PM" src="https://github.com/user-attachments/assets/448fa11c-22cf-450b-9091-2a7ba2ee9f48" />

<p>Now that I’ve got the virtual machine created, I’m just copying the public IP address of the VM. I’ll need this to connect to it in the next step.</p>

<p><img width="800" alt="Screenshot 2025-06-18 at 10 57 38 AM" src="https://github.com/user-attachments/assets/b44f7708-4e25-49bf-8874-7d5d7d782b9f" />

</p>
<p>
Since I’m on a Mac, I downloaded the Windows App so I can use RDP to connect. But if you’re on Windows, you can just go ahead and use the built-in Remote Desktop app. Go ahead and paste the public ip address and open up the VM. 

</p>
<br />

<img width="800" alt="Screenshot 2025-06-18 at 10 50 58 AM" src="https://github.com/user-attachments/assets/0c586f2d-de01-47de-8718-a59f09db9b46" />

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
