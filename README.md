<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This guide documents the setup and configuration of the open-source help desk ticketing system **osTicket**, hosted on a Microsoft Azure virtual machine running Windows Server and IIS.

---

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines / Compute)
- Remote Desktop (RDP)
- Internet Information Services (IIS)
- PHP 7.3.8
- MySQL 5.5.62
- HeidiSQL 12.3.0.6589
- osTicket v1.15.8

---

<h2>Operating Systems Used</h2>

- Windows 10 Enterprise N </b> (22H2)

---

<h2>List of Prerequisites</h2>

- Microsoft Azure subscription and active VM
- Windows IIS and CGI enabled
- PHP Manager for IIS installed
- URL Rewrite Module installed
- PHP 7.3.8 configured in IIS
- Microsoft Visual C++ runtime Installed
- MySQL 5.5.62 installed and running
- HeidiSQL for database management
- osTicket installation files extracted to IIS web root

---

<h2>Installation Steps</h2>


<p>
<strong>Step 1 – Enable IIS and CGI:</strong><br/>
From Control Panel, go to Programs, add the IIS role, and include the CGI feature under Application Development Features in the World Wide Web Services. This enables PHP to run on the web server through FastCGI, a requirement for osTicket.
</p>
<p>
  <img src="https://i.imgur.com/lvt8SfC.png" height="80%" width="80%" alt="Enable IIS and CGI"/>
</p>
<br />


<p>
<strong>Step 2 – Install Dependencies:</strong><br/>
Install PHP Manager for IIS and the URL Rewrite Module from the provided installation files. These components ensure IIS can interpret PHP and handle dynamic web content correctly.
</p>
<p>
  <img src="https://i.imgur.com/rXy749I.png" height="80%" width="80%" alt="Install PHP Manager"/>

Using the PHP install wizard install PHP
  
  <img src="https://i.imgur.com/2fbT3OU.png" height="80%" width="80%" alt="Install URL Rewrite Module"/>

With the URL Rewrite Module install URL Rewrite
  
</p>
<br />


<p>
<strong>Step 3 – Configure PHP:</strong><br/>
Extract the provided PHP 7.3.8 package to <code>C:\PHP</code>. Verify Files Extracted Correctly into <code>C:/PHP</code>
</p>
<p>
  <img src="https://i.imgur.com/qNUjfVr.png" height="80%" width="80%" alt="PHP Setup Before Extract"/>
  <img src="https://i.imgur.com/utMdGwq.png" height="80%" width="80%" alt="PHP Setup After Extract"/>
</p>
<br />


<p>
<strong>Step 4 – Install VC_redist.x86.exe for Microsoft C++:</strong><br/>
Install VC_redist.x86.exe which installs the Microsoft Visual C++ runtime dependencies required by PHP to operate under IIS. It ensures stable and compatible PHP execution for the osTicket application.
</p>
<p>
  <img src="https://i.imgur.com/vsG0zXV.png height="80%" width="80%" alt="MySQL Installation"/>
</p>
<br />


<p>
<strong>Step 5 – Install and Configure MySQL:</strong><br/>
Install MySQL 5.5.62 with standard configuration. Set a username & password then confirm that the MySQL service is running. This database server will store osTicket’s ticketing and user data.
</p>
<p>
  <img src="https://i.imgur.com/TBXJX8X.png" height="80%" width="80%" alt="MySQL Post Install Wizard"/>
  <img src="https://i.imgur.com/mGOk1x0.png" height="80%" width="80%" alt="MySQL Account Setup "/>
  <img src="https://i.imgur.com/zyDxcKV.png" height="80%" width="80%" alt="MySQL server Configuration"/>
</p>
<br />


<p>
<strong>Step 6 – Register PHP within IIS:</strong><br/>
To make the Web Server aware of PHP on the computer. Register PHP from within IIS under Administrator Access. PHP Manager -> <code>C:\PHP\php-cgi.exe</code> After Registering the PHP restart the Server.
</p>
<p>
  <img src="https://i.imgur.com/o2vOtoK.png" height="80%" width="80%" alt="IIS Search (Run as Administrator"/>

Run as Administrator
  
  <img src="https://i.imgur.com/KaHm2sZ.png" height="80%" width="80%" alt="IIS Menu (PHP Manager)"/>

Access PHP Manager
  
  <img src="https://i.imgur.com/8OdZRak.png" height="80%" width="80%" alt="PHP Manager before Register"/>

Select Register New PHP Version
  
  <img src="https://i.imgur.com/Ydm4xgV.png" height="80%" width="80%" alt="PHP Manager at Register"/>

Serach in the C: Drive in the PHP file we made earlier for php-cgi.exe

</p>
<br />


<p>
<strong>Step 7 – Deploy osTicket Files:</strong><br/>
Copy the “upload” folder from the osTicket installation files to <code>C:\inetpub\wwwroot</code> and rename it to <code>osTicket</code>. Restart IIS and confirm the folder is accessible at <code>http://localhost/osTicket</code>.
</p>
<p>
  <img src="https://i.imgur.com/olif1kl.png" height="80%" width="80%" alt="Extract osTicket Files"/>

Extract osTicket Files
  
  <img src="https://i.imgur.com/dpaaura.png" height="80%" width="80%" alt="Copy Upload to C Drive inetpub\wwwroot"/>

Copy Upload File to C:\inetpub\wwwroot
  
  <img src="https://i.imgur.com/9EqpCB9.png" height="80%" width="80%" alt="Change name of Folder to osTicket"/>

Change name of folder to osTicket, after this restart the IIS Server
  
</p>
<br />

<p>
<strong>Step 8 – Enable PHP Extensions:</strong><br/>
Within PHP Manager, enable <code>php_imap.dll</code>, <code>php_intl.dll</code>, and <code>php_opcache.dll</code>. Restart IIS to apply changes. These extensions are required for email integration, localization, and performance caching.
</p>
<p>
<img src="https://i.imgur.com/EuRnFxL.png" height="80%" width="80%" alt="osTicket Web Site Page"/>

In IIS access osTicket under Sites->Default Web Site and Select Browse *:80

<img src="https://i.imgur.com/VZj20Qo.png" height="80%" width="80%" alt="osTicket Web Site"/>

This Web Page will open allowing you to install osTicket, First we need to add Extensions

<img src="https://i.imgur.com/WcPyx6t.png" height="80%" width="80%" alt="osTicket PHP Manager Extension Change"/>

In IIS, inside osTicket access PHP Manager and Select Enable or disable extension then enable php_imap.dll, php_intl.dll, & php_opcache.dll.

<img src="https://i.imgur.com/24F8L9s.png" height="80%" width="80%" alt="osTicket Installer after Extension Enabled"/>

Refresh the osTicket Installer Web Page to see three of the missing extensions have been enabled.

<img src="https://i.imgur.com/uG2NQVr.png" height="80%" width="80%" alt="ost-config Rename"/>

Inside the C drive->inetpub->wwwroot->osTicket->Include search for ost-sampleconfig.php and rename it to ost-config.php

<img src="https://i.imgur.com/zMGQiRo.png" height="80%" width="80%" alt="Disable Inheritance"/>

Access the ost-config.php Properties and disable Inheritance removing all objects

<img src="https://i.imgur.com/5aVzbxY.png" height="80%" width="80%" alt="Add Everyone for Permissionss"/>

Alter Permissions to give Everyone Full Access to the System
  
</p>
<br />


<p>
<strong>Step 9 – Create the Database:</strong><br/>
Using HeidiSQL, connect to MySQL with your root credentials. Create a new database named <code>osTicket</code>. This will store all help desk tickets, users, and system settings.
</p
<p>
<img src="https://i.imgur.com/6gaVp3w.png" height="80%" width="80%" alt="Install HeidiSQL"/>

Install HeidiSQL

<img src="https://i.imgur.com/racucnY.png" height="80%" width="80%" alt="Run HeidiSQL"/>

After installing HeidiSQL, Run it

<img src="https://i.imgur.com/0DYo8HC.png" height="80%" width="80%" alt="Login to HeidiSQL"/>

Using the login you made during the configuration sign into HeidiSQL

<img src="https://i.imgur.com/D3M8DlB.png" height="80%" width="80%" alt="Make a new osTicket Database"/>

Insidr HeidiSQL, make a new database under the name of "osTicket" then return back to the Installer

<img src="https://i.imgur.com/6YLVzSm.png" height="80%" width="80%" alt="osTicket Account set up"/>

Fill out the information to make the osTicket Account. Input your newly made SQL information into the Database Settings then click Install

<img src="https://i.imgur.com/ExSMm9l.png" height="80%" width="80%" alt="osTicket login"/>

Attempt to login into the adminuser account that was made by going to [localhost/osTicket](http://localhost/osTicket/scp/login.php). Use adminuser and password created.

</p>
<br />


<p>
<strong>Step 10 – Post-Installation Security:</strong><br/>
Delete the <code>setup</code> folder in the osTicket directory and set <code>ost-config.php</code> to read-only. Log into the admin panel and verify you can create, assign, and resolve tickets.
</p>
<p>
<img src="https://i.imgur.com/nSLsY6k.png" height="80%" width="80%" alt="Delete Setup Folder"/>

Delete the Setup Folder inside inetpub\wwwroot\osTicket in the C Drive

<img src="https://i.imgur.com/yavlkzr.png" height="80%" width="80%" alt="Change ost-config to Read Only"/>

Change the ost-config.php settings to be Read Only
  
</p>
<br />

---

<h2>Final Verification</h2>

- Public Portal: <code>http://localhost/osTicket</code>  
- Admin Portal: <code>http://localhost/osTicket/scp</code>  
- Confirmed successful ticket creation, assignment, and resolution.  
- Verified IIS, PHP, and MySQL services are active.

---

<h2>End Result</h2>
A fully functional osTicket deployment demonstrating configuration of a web application stack (IIS, PHP, MySQL) within an Azure-hosted Windows environment. This project highlights core skills in system setup, troubleshooting, and environment management.
