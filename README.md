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
<br />
<p>
Since I’m on a Mac, I downloaded the Windows App so I can use RDP to connect. But if you’re on Windows, you can just go ahead and use the built-in Remote Desktop app. Go ahead and paste the public ip address and open up the VM. 

</p>
<br />

<img width="800" alt="Screenshot 2025-06-18 at 10 50 58 AM" src="https://github.com/user-attachments/assets/0c586f2d-de01-47de-8718-a59f09db9b46" />

<br />

<p>
I just copied and pasted the osTicket-Installation-Files.zip link into the web browser inside the osTicket VM to download the files I need for osTicket.

Once it’s downloaded, I just open up File Explorer, go to Downloads, and drag the osTicket-Installation-Files.zip over to the Desktop. After that, I go ahead and unzip it right there on the desktop.

</p>
<br />


<img width="800" alt="Screenshot 2025-06-20 at 1 52 01 PM" src="https://github.com/user-attachments/assets/251ddc71-de4c-4b98-a764-a4f0a4b65825" />

<h4>Install / Enable IIS in Windows WITH CGI
</h4>
<p>So I click on the Start menu, go to Control Panel, then into Programs. From there, I click "Uninstall a program", and then hit "Turn Windows features on or off."
  
Once I’ve got that open, I enable **IIS (Internet Information Services)**. Then I expand **World Wide Web Services**, expand it again, go into **Application Development Features**, and check the box for **CGI**. It should look like this. After pressing OK, the server will be installed. 

</p>

<img width="1700" alt="Screenshot 2025-06-18 at 1 03 23 PM" src="https://github.com/user-attachments/assets/40b89a8d-33a5-45e7-80d6-14090ac3a589" />

<P>After it’s done installing, I check the loopback IP (127.0.0.1) just to make sure it’s working, and it should look like this.

</P>

<img width="900" alt="Screenshot 2025-06-20 at 2 24 32 PM" src="https://github.com/user-attachments/assets/6ba32f7d-5813-479b-b0a8-8ab5c55da999" />

<br />

<h4>From the “osTicket-Installation-Files” folder, install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)
</h4>

<p>So I’m downloading PHP Manager for IIS because osTicket runs on PHP, which is the backend language that handles all the ticket processing and database stuff. PHP Manager makes it easier to set up PHP inside IIS so everything works properly. I just click yes on everything and install.

</p>

<img width="900" alt="Screenshot 2025-06-20 at 10 00 56 PM" src="https://github.com/user-attachments/assets/fe765964-5dec-4780-83b4-70a34d34db94" />

<h4>Install the Rewrite Module (rewrite_amd64_en-US.msi) 

</h4>  

<p>I’m installing it because osTicket uses clean URLs, and without this, IIS wouldn’t know how to handle those URLs properly. The Rewrite Module basically helps IIS understand how to route everything so osTicket works the way it’s supposed to.</p>

<img width="1200" alt="Screenshot 2025-06-20 at 10 00 56 PM" src="https://github.com/user-attachments/assets/abccb504-7c05-49ec-8b14-0b7e65a2c98e" />

<h4>Create the directory C:\PHP</h4>

<p>From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder
</p>

<p>I’m extracting all the PHP files into that folder. This is where IIS and osTicket are gonna pull the PHP files from to run everything.
</p>

<p>Create the PHP Folder in the c drive</p>

 <img width="1200" alt="Screenshot 2025-06-21 at 12 02 37 AM" src="https://github.com/user-attachments/assets/ff551c47-e542-40a7-929c-71aad3f007d0" />

 <p>Then I right-click on php-7.3.8-nts-Win32-VC15-x86.zip, click Extract All, and choose the PHP folder. You can just type C:\PHP or click Browse → This PC → Windows (C:) → PHP to select the folder.

</p>

<img width="1593" alt="Screenshot 2025-06-21 at 12 08 34 AM" src="https://github.com/user-attachments/assets/8f89c867-3658-4075-83d3-1b447570595c" />

<h4>From the “osTicket-Installation-Files” folder, install VC_redist.x86.exe</h4>
<p>This is the Microsoft Visual C++ Redistributable package. VC_redist.x86.exe installs required runtime files that allow PHP (and osTicket) to run smoothly on Windows.

</p>

<img width="900" alt="Screenshot 2025-06-21 at 9 16 59 AM" src="https://github.com/user-attachments/assets/2e781f8d-e93b-419e-9ae1-dd4af38bfcdc" />

<h4>From the “osTicket-Installation-Files” folder, install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
</h4>
<p>This is what osTicket uses to store all the tickets, users, and everything else. Basically, MySQL is the database that keeps track of everything behind the scenes. 
  
Make sure to choose "typical" for the set up type then install.
</p>

<img width="900" alt="Screenshot 2025-06-21 at 9 23 10 AM" src="https://github.com/user-attachments/assets/e66b2922-a9d5-4227-845a-d3c5031ec5d3" />

<p>Launch Configuration Wizard (after install) -> Choose Standard Configuration, then hit next, you can leave the next one alone and go create the password  </p>

<img width="499" alt="Screenshot 2025-06-21 at 9 45 57 AM" src="https://github.com/user-attachments/assets/22ab39d3-a895-4657-8f3e-02ae8a6e16c5" />

<h4>It’s crucial to keep the password simple for this setup, so I just use "root" as the password. Obviously, this is really bad practice in real life, but to keep things simple for this project, I’m using "root". The main reason I’m doing this is because people tend to forget the password when setting this up, and it saves me the headache of getting locked out while testing.

 </h4>

<img width="499" alt="Screenshot 2025-06-21 at 9 39 09 AM" src="https://github.com/user-attachments/assets/e1135005-2271-4b42-9459-c27461bb9d1f" />

<p>So I just click next, we don't really have to do anything else so just execute.</p>

<img width="499" alt="Screenshot 2025-06-21 at 9 42 28 AM" src="https://github.com/user-attachments/assets/5c0ab8f7-215a-4503-86f1-c426b86b4a51" />

<p>So now we’ve got the database installed. Right now, it’s just an empty database, nothing’s configured yet, but it’s there and ready for us to set up when we get to that part.</p>

<img width="499" alt="Screenshot 2025-06-21 at 9 47 49 AM" src="https://github.com/user-attachments/assets/a016c1a4-580b-4889-80ee-d45f837594e7" />



<h4>Open IIS as an Admin</h4>

<p>So next up, I’m opening up IIS as an admin, and now I’m gonna start messing around inside my web server. I’m gonna configure PHP and do a few other things that osTicket needs to get everything running properly. </p>

So i just go start menu -> type "iss" on the search bar -> either right click and run as admin or click run as administrator on the right side.

<img width="900" alt="Screenshot 2025-06-21 at 9 56 59 AM" src="https://github.com/user-attachments/assets/5374110a-2685-4ff9-8444-0d57e5f061c5" />

<h4>Register PHP from within IIS (PHP Manager -> C:\PHP\php-cgi.exe)</h4>

<p>So we’re doing this so the web server actually knows that PHP exists on the computer. We’re basically just telling IIS where PHP is located so it knows how to handle any PHP files that come through.
  
So I'm going to first open PHP Manager
</p>

<img width="854" alt="Screenshot 2025-06-21 at 10 12 43 AM" src="https://github.com/user-attachments/assets/5a93bde6-2835-4d55-88c1-9c4250a1c003" />

<p>Click "Register new PHP version"</p>

<img width="854" alt="Screenshot 2025-06-21 at 10 12 43 AM" src="https://github.com/user-attachments/assets/87b467b1-6376-4e50-8454-1c9f587cbc80" />

<p>Then I'm going to browse for the PHP folder that i just made in the c drive 
Click ... -> This PC -> PHP -> Then run php.cgi
</p>

<img width="849" alt="Screenshot 2025-06-21 at 2 43 03 PM" src="https://github.com/user-attachments/assets/e6250665-7bc7-49a6-a2a1-c1a33e54d2cb" />









