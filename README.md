<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This guide covers the requirements and installation process for the open-source osTicket help desk ticketing system.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Windows Server or Windows 10 (21H2) – A compatible operating system to host osTicket.

- Internet Information Services (IIS) – Web server to serve the osTicket application.

- PHP – Required to run osTicket scripts.

- MySQL – Database server for storing ticketing system data.

- osTicket Installation Files – Downloadable from the official osTicket website or down below in the installation steps.

<h2>Installation Steps</h2>


![#1](https://github.com/user-attachments/assets/14b13ed2-f84f-49aa-98ac-1fd2c766b6a9)

<p>
Step 1 : Setting Up a Virtual Machine in Azure

To create a Virtual Machine (VM) in Microsoft Azure, start by logging into the Azure Portal and navigating to the Virtual Machines section. Click Create and select a Resource Group, or create a new one (e.g., "osTicket"). Name your VM (e.g., "osticket-VM") and choose a region.

Next, select Windows 10 Pro, version 22H2 - x64 Gen2 as the OS image and pick a VM size with at least 2 vCPUs. Create a username and password for login. Proceed to the Networking section, where Azure will generate a virtual network automatically—leave settings as default or modify if needed.

Finally, review your selections and click Create. Once the VM is deployed, connect via RDP using the assigned credentials. Your Azure VM is now ready to use!
</p>
<br />

<p>

![2](https://github.com/user-attachments/assets/c51e5d2f-76a9-4700-b77d-fad00883eb5f)

</p>
<p>
Step 2 : Connecting to Your Azure Virtual Machine via RDP

After creating your Azure Virtual Machine (VM), you will connect to it using Remote Desktop (RDP). First, retrieve the public IP address by navigating to the Virtual Machines section in the Azure Portal—the public IP will be displayed on the right side.

Next, open Remote Desktop Connection (RDP) on your Windows computer, enter the public IP, and click Connect. On the login page, select "More choices", then "Use a different account". Enter the username and password you created during VM setup, then log in.
</p>
<br />

<p>

![3](https://github.com/user-attachments/assets/100f06db-b71e-4372-9728-d8fc685ac39a)

</p>
<p>
Step 3 : Installing osTicket and Enabling IIS with CGI
  
After logging into your Azure Virtual Machine (osticket-VM), open Microsoft Edge and download the osTicket installation files using the following link:

[🔗 osTicket Installation Files](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

Once downloaded, unzip the file onto your desktop. Right-click the "osTicket-Installation-Files" folder, select "Extract All", and extract it.

Next, install Internet Information Services (IIS) with CGI:

Open the Control Panel and go to Programs → Uninstall a Program.

On the left side, click "Turn Windows features on or off".

Find and check "Internet Information Services (IIS)".

Expand "World Wide Web Services", then expand "Application Development Features", and check the CGI box.

![also3](https://github.com/user-attachments/assets/5a91c09c-9d13-46d5-9283-2cc73ddf711d)


Click OK to install IIS and enable the web server.
</p>
<br />

<p>

![4](https://github.com/user-attachments/assets/6eb6aef1-03f1-4a1e-89d8-526d422716e4)

</p>
<p>
Step 4 : Installing PHP Manager for IIS, Rewrite Module, and Setting Up PHP

Install PHP Manager for IIS

Open the osTicket-Installation-Files folder.

Locate PHP Manager and run the installer.

Click Yes on all prompts to complete the installation.

Install IIS Rewrite Module

In the same folder, find the Rewrite Module installer.

Run the installer and follow the setup instructions.

Create a PHP Directory on C: Drive

Open File Explorer and go to **C:**.

Create a new folder named PHP.

Extract PHP 7.3.8 into the PHP Folder

In the osTicket-Installation-Files folder, find PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip).

Right-click it, select Extract All, and choose C:\PHP as the destination.

Click Extract to complete the process.
</p>
<br />

<p>

![5](https://github.com/user-attachments/assets/f3f348f1-2118-442c-89e7-0066566a6e53)

</p>
<p>
Step 5 : Installing VC Redistributable and MySQL

Install VC Redistributable

Open the osTicket-Installation-Files folder.

Locate the VC Redistributable file and run the installer.

Follow the prompts to complete the installation.

Install MySQL

In the same folder, find the MySQL installer and run it.

On the Choose Setup Type screen, select Typical and click Install.

Click Yes when prompted to allow MySQL to make changes to your device.

Configure MySQL

Before finishing the installation, ensure the "Launch the MySQL Instance Configuration Wizard" box is checked.

Click Finish, and if prompted again, allow MySQL InstanceConfig to make changes.

In the MySQL Server Instance Configuration Wizard, click Next until you reach the Configuration Type screen.

Select Standard Configuration and continue clicking Next until you reach Security Settings.

Set a new root password, confirm it, then click Next and Execute to finalize the setup.
</p>
<br />

<p>

![6](https://github.com/user-attachments/assets/006ca7d6-1395-4df7-ab39-e1eab4d1bcde)

</p>
<p>
Step 6 : Configuring IIS and Registering PHP

Open IIS as Administrator

Click Start, search for IIS (Internet Information Services Manager).

Right-click it and select Run as Administrator.

Register PHP in IIS

Open PHP Manager within IIS.

Click Register new PHP version.

Click the three dots (…) to browse to C:\PHP.

![6too](https://github.com/user-attachments/assets/a16483cc-f9ab-42f9-8b90-5bb50679bf61)


Select the php-cgi file and click OK.

Reload IIS

In IIS Manager, locate osticket-VM on the upper left.

Right-click it and select Stop.

Wait a moment, then right-click it again and select Start.
</p>
<br />

<p>

![7](https://github.com/user-attachments/assets/285ecb9a-7d0e-4081-abdf-d99d729b10a4)

</p>
<p>
Step 7 : Installing osTicket and Configuring IIS
  
Extract osTicket Files

Open the osTicket-Installation-Files folder.

Extract the osticket folder—this will create a new folder named osticket inside the same directory.

Move the Upload Folder

Open the newly created osticket folder.

Inside, locate the upload folder.

Open File Explorer, navigate to C:\inetpub\wwwroot.

Drag and drop the upload folder into wwwroot.

Rename the upload folder to osTicket (ensure exact spelling to avoid issues).

Reload IIS

If IIS Manager is open, right-click osticket-VM in the upper left corner, select Stop, wait a moment, then select Start.

If IIS is closed, search IIS in the Windows menu, right-click, and Run as Administrator, then restart the server as mentioned.
</p>
<br />

<p>

![8](https://github.com/user-attachments/assets/1fe6942f-a65b-4cb8-addb-12c667f36334)

</p>
<p>
Step 8 : Loading osTicket and Enabling Required PHP Extensions

Load the osTicket Site

Open IIS Manager and expand Sites.

Expand Default Web Site and click on the osTicket folder.

On the right, under Manage Folder, click Browse *:80 (http).

The osTicket setup page should load in your browser.

Enable Required PHP Extensions

Go back to IIS Manager and navigate to the osTicket folder under Default Web Site.

Open PHP Manager.

Scroll down to PHP Extensions, then click Enable or Disable an Extension.

Locate and enable the following extensions:

php_imap.dll

php_intl.dll

php_opcache.dll

To enable each, right-click it and select Enable.
</p>
<br />

<p>

![9](https://github.com/user-attachments/assets/b4e6ae92-6b02-49e1-9cd9-c6431ac59e25)

</p>
<p>
Step 9 : Configuring osTicket Configuration File
Rename Configuration File

Open File Explorer and navigate to:
C:\inetpub\wwwroot\osTicket\include

Locate ost-sampleconfig.php.

Right-click it and rename it to ost-config.php.

Modify Security Permissions

Right-click ost-config.php and select Properties.

Go to the Security tab and click Advanced.

Click Disable inheritance → Remove all inherited permissions from this object.

Click Add, then Select a principal.

In the Object name field, type everyone, then click OK.

Check the Full control box under Basic permissions, then click OK.

Click Apply and OK to save changes.
</p>
<br />

<p>

![10](https://github.com/user-attachments/assets/e903df47-6e8b-4f88-81dd-77dc3cb4c6bc)

</p>
<p>
Step 10 : Completing osTicket Setup and Installing HeidiSQL
Access the osTicket Setup Page

Open a web browser and go to:
localhost/osTicket/setup/

Click Continue at the bottom to proceed with the setup.

Enter Helpdesk Information

Fill in the Helpdesk Name (can be any name).

The Email Address does not need to be real.

Set Up the Admin User

Enter a Username (e.g., adminuser).

Enter a Password (e.g., Password1).

Install HeidiSQL

Open File Explorer and navigate to your Desktop.

Open the osTicket-Installation-Files folder.

Locate HeidiSQL and run the installer.
</p>
<br />

<p>

![11](https://github.com/user-attachments/assets/c3bacf2d-1e69-4745-b086-539fc56de638)

</p>
<p>
Step 11 : Configuring HeidiSQL and Creating the osTicket Database
Open HeidiSQL

After installation, HeidiSQL should launch automatically.

Click New at the bottom to create a new connection.

Log into MySQL

On the right side, enter:

Username: root

Password: (use the root password set during MySQL installation)

Click Open to connect to the database.

Create the osTicket Database

In the left panel, right-click on Unnamed.

Select Create New → Database.

Name the database osTicket and confirm.
</p>
<br />

<p>

![12](https://github.com/user-attachments/assets/c293b880-23c8-4ba8-b6a1-d7a7db7ce99b)

</p>
<p>
Step 12 : Finalizing osTicket Installation
Return to the osTicket Setup Page

Open your web browser and go back to the osTicket setup page.

If needed, navigate to localhost/osTicket/setup/.

Enter Database Settings

MySQL Database Name: osTicket

MySQL Username: root

MySQL Password: root
Complete the Installation

Click Install Now to finalize the setup.
Congratulations, hopefully it is installed with no errors!

Browse to your help desk login page: http://localhost/osTicket/scp/login.php

End Users osTicket URL:
http://localhost/osTicket/ 

</p>
<br />
