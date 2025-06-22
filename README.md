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

<img width="868" alt="Screenshot 2025-06-21 at 2 38 46 PM" src="https://github.com/user-attachments/assets/85d2cdd5-2988-4ac8-b3b5-00d4147185c8" />


<p>Then I'm going to browse for the PHP folder that I just made in the c:\ drive 
Click ... -> This PC -> c:\ PHP -> Then run php.cgi
</p>

<img width="849" alt="Screenshot 2025-06-21 at 2 43 03 PM" src="https://github.com/user-attachments/assets/e6250665-7bc7-49a6-a2a1-c1a33e54d2cb" />

<h4>Reload IIS (Open IIS, Stop and Start the server)
</h4>

<p>So after registering PHP inside IIS, I go ahead and reload IIS — I just open up IIS, stop the server, and start it again. This makes sure all the changes take effect.

</p>

<img width="855" alt="Screenshot 2025-06-22 at 11 03 25 AM" src="https://github.com/user-attachments/assets/94992656-8f30-496e-9447-7562a3999d3e" />


<img width="855" alt="Screenshot 2025-06-22 at 11 03 44 AM" src="https://github.com/user-attachments/assets/eea248d9-320a-4b5f-bee6-288baeec4c17" />

<h4>Install osTicket v1.15.8
</h4>

<p>From the “osTicket-Installation-Files” folder, unzip “osTicket-v1.15.8.zip”</p>

<img width="855" alt="Screenshot 2025-06-22 at 11 08 42 AM" src="https://github.com/user-attachments/assets/5c96cacb-7adc-4c6d-89af-1982514f8cbc" />

<img width="616" alt="Screenshot 2025-06-22 at 11 10 24 AM" src="https://github.com/user-attachments/assets/dc94de70-cc72-4e22-a488-8943a57c496d" />

<img width="854" alt="Screenshot 2025-06-22 at 11 17 28 AM" src="https://github.com/user-attachments/assets/e30e58bc-a1d0-4c92-a558-10b57700a510" />

<h4>Copy the “upload” folder into “c:\inetpub\wwwroot”</h4>
<p>Inside the osTicket-v1.15.8 folder we extracted earlier, I’m grabbing the upload folder and moving it into C:\inetpub\wwwroot.</p>

<h4>So I opened up file explorer -> This PC -> Windows (C:) -> inetpub -> wwwroot</h4>

<img width="900" alt="Screenshot 2025-06-22 at 11 46 08 AM" src="https://github.com/user-attachments/assets/eaa31a48-567b-4434-8ba9-277b3d60e9fd" />

<img width="900" alt="Screenshot 2025-06-22 at 11 46 17 AM" src="https://github.com/user-attachments/assets/bcc36020-6feb-47a7-b2e0-d11fbd0c02f1" />

<h4>Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”
</h4>

<p>After moving it, I make sure to rename the upload folder to just osTicket — no spaces, nothing extra, it should just be exactly "osTicket". </p>

<img width="855" alt="Screenshot 2025-06-22 at 11 53 09 AM" src="https://github.com/user-attachments/assets/38d2b620-7c6e-4e93-8da6-3c6d8939ecea" />

<h4>Reload IIS (Open IIS, Stop and Start the server)
</h4>
<p>Now I go ahead and reload IIS again — just open IIS, stop the server, and start it back up to make sure it picks up the changes we just made. </p>

<img width="855" alt="Screenshot 2025-06-22 at 11 03 25 AM" src="https://github.com/user-attachments/assets/6628c677-6cee-430f-b136-94269b6b69b4" />

<img width="855" alt="Screenshot 2025-06-22 at 11 03 44 AM" src="https://github.com/user-attachments/assets/b1c2131d-fba3-41de-ac1f-1c41daf587d5" />

<h4>Now I'm going to try loading up the osTicket site. I go to Sites → Default → osTicket inside IIS. Then on the right side, I click *“Browse:80” to open it up.

</h4>

<img width="1048" alt="Screenshot 2025-06-22 at 12 06 27 PM" src="https://github.com/user-attachments/assets/f9a39f25-2515-47e5-9b2d-140fdb6097e6" />

<p>After opening it up, it should load and look something like this. </p>

![Screenshot 2025-06-22 at 12 12 59 PM](https://github.com/user-attachments/assets/e76d283e-ae5e-42e8-a8ea-de73b519839f)

<p>You’ll notice that some extensions aren’t enabled yet. So I go back into IIS → Sites → Default → osTicket, then double-click PHP Manager. From there, I click “Enable or disable an extension” and enable the following: php_imap.dll, php_intl.dll, and php_opcache.dll.

</p>
<img width="851" alt="Screenshot 2025-06-22 at 5 28 42 PM" src="https://github.com/user-attachments/assets/3b2a50da-570e-4a74-859d-a0d6a24f51af" />

<img width="851" alt="Screenshot 2025-06-22 at 5 31 41 PM" src="https://github.com/user-attachments/assets/f868f76a-cce9-4279-86d1-48373f960e6e" />

<p>You can either right-click on each extension and hit Enable, or just select it and press Enable on the top right corner.

</p>

<img width="851" alt="Screenshot 2025-06-22 at 5 38 17 PM" src="https://github.com/user-attachments/assets/583dc259-cca1-4b46-9c8a-814262b9e1ef" />

<p>After we’ve enabled those extensions, I just refresh the osTicket website, and now I can see that all the extensions we enabled are checked off and ready to go.

</p>
<img width="833" alt="Screenshot 2025-06-22 at 5 45 21 PM" src="https://github.com/user-attachments/assets/d1abd978-f1a3-4abe-b3e7-94d62445ef0b" />

<p>Next up, I’m renaming a file that osTicket uses for its configuration. Basically, I’m taking ost-sampleconfig.php from C:\inetpub\wwwroot\osTicket\include\ and renaming it to ost-config.php. This is the file osTicket is gonna use to store all the config settings.

</p>

<img width="851" alt="Screenshot 2025-06-22 at 5 58 58 PM" src="https://github.com/user-attachments/assets/f095e565-ef55-469a-b71d-f04188c502f9" />

<p>Next, I’m assigning permissions to the ost-config.php file. I go in, disable inheritance, and remove all the existing permissions. Then I add new permissions and give Everyone full access.

So first, I right-click on ost-config.php and click Properties. Once it opens up, it should look like this.
</p>

<img width="900" alt="Screenshot 2025-06-22 at 6 08 49 PM" src="https://github.com/user-attachments/assets/30f7adf9-ebee-43c9-a4cf-bbd6dae80c1a" />
<p>Then I click on the Security tab inside the ost-config.php Properties, and from there I click Advanced to get into the permission settings.

</p>
<img width="361" alt="Screenshot 2025-06-22 at 6 12 17 PM" src="https://github.com/user-attachments/assets/79641e91-5365-4fd3-a931-f0b6800bb1da" />

<p>So now I’m gonna disable inheritance to strip away all the previous permissions that were already set on the file.

</p>

<img width="765" alt="Screenshot 2025-06-22 at 6 16 22 PM" src="https://github.com/user-attachments/assets/bdabc3e6-9daa-4a67-9aec-a7fbcf7e5437" />
<img width="765" alt="Screenshot 2025-06-22 at 6 16 42 PM" src="https://github.com/user-attachments/assets/20f7f6d7-d9c3-4dd9-8417-a1d8576b1052" />
<p>Now I'm going to add new permissions.</p>
<img width="765" alt="Screenshot 2025-06-22 at 6 19 09 PM" src="https://github.com/user-attachments/assets/d5774c6b-e3ae-4631-8089-eba37edb36e9" />
<p>Click Select a Principal</p>
<img width="914" alt="Screenshot 2025-06-22 at 6 24 09 PM" src="https://github.com/user-attachments/assets/66dbbad6-149b-49ef-bedf-3575a605524e" />
<p>So now I’m adding new permissions. This isn’t something you’d want to do in real life, but just to keep it simple for this setup, I’m giving Everyone full access since I don’t know exactly which user osTicket is running as.</p>

<img width="914" alt="Screenshot 2025-06-22 at 6 28 14 PM" src="https://github.com/user-attachments/assets/71717858-f9c2-4e42-ba41-f2c465f08ed3" />
<p>Then check full control and hit OK.</p>
<img width="914" alt="Screenshot 2025-06-22 at 6 30 05 PM" src="https://github.com/user-attachments/assets/c8ad3863-d51e-45f0-8a99-63d0cef0a449" />
<p>So after everything’s done, it should look like this -> ost-config.php with Everyone having full access.

Then click apply and then OK </p>
<img width="765" alt="Screenshot 2025-06-22 at 6 33 04 PM" src="https://github.com/user-attachments/assets/098dec18-2007-4a84-bc56-104fefdb997f" />
<p>And click OK here as well</p>
<img width="362" alt="Screenshot 2025-06-22 at 6 34 17 PM" src="https://github.com/user-attachments/assets/04cf18bd-9756-4dfc-94ff-d898d68525d0" />

<p>Then, after that, I head back to the osTicket website and continue with the setup from there.</p>
<img width="823" alt="Screenshot 2025-06-22 at 6 38 35 PM" src="https://github.com/user-attachments/assets/298b3ef4-95a9-4f9e-99c1-e8cf69c29e0d" />

<p>Then you can name the Help Desk whatever you want, for mine, I just went with Reimon's Help Desk. Same with the email, it can be anything you want since this is just for the lab setup.

And for the admin user, same thing, you can just put your name and last name. The only thing is that the email address needs to be different from the help desk email.

And for the username and password, I just went with username: adminuser and password: Password1, just to keep things easy for this project.

Before we click Install, even though we’ve already installed the database application on the backend, we still need to actually log into that database and create a new database specifically for osTicket. After that, we’ll provide the credentials for this section so osTicket knows where to store everything.

</p>
<img width="1000" alt="Screenshot 2025-06-22 at 6 49 31 PM" src="https://github.com/user-attachments/assets/c9b270b5-87e3-48cc-ba63-0d76e45ac944" />












