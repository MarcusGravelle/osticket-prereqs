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
  <img src="https://i.imgur.com/lvt8SfC.png" height="80%" width="80%" alt="Enable IIS and CGI"/>
</p>
<p>
<strong>Step 1 – Enable IIS and CGI:</strong><br/>
From Control Panel, go to Programs, add the IIS role, and include the CGI feature under Application Development Features in the World Wide Web Services. This enables PHP to run on the web server through FastCGI, a requirement for osTicket.
</p>
<br />

<p>
  <img src="https://i.imgur.com/rXy749I.png" height="80%" width="80%" alt="Install PHP Manager"/>
  <img src="https://i.imgur.com/2fbT3OU.png" height="80%" width="80%" alt="Install URL Rewrite Module"/>
</p>
<p>
<strong>Step 2 – Install Dependencies:</strong><br/>
Install PHP Manager for IIS and the URL Rewrite Module from the provided installation files. These components ensure IIS can interpret PHP and handle dynamic web content correctly.
</p>
<br />

<p>
  <img src="https://i.imgur.com/qNUjfVr.png" height="80%" width="80%" alt="PHP Setup Before Extract"/>
  <img src="https://i.imgur.com/utMdGwq.png" height="80%" width="80%" alt="PHP Setup After Extract"/>
</p>
<p>
<strong>Step 3 – Configure PHP:</strong><br/>
Extract the provided PHP 7.3.8 package to <code>C:\PHP</code>. Verify Files Extracted Correctly into <code>C:/PHP</code>
</p>
<br />

<p>
  <img src="https://i.imgur.com/vsG0zXV.png height="80%" width="80%" alt="MySQL Installation"/>
</p>
<p>
<strong>Step 4 – Install VC_redist.x86.exe for Microsoft C++:</strong><br/>
Install VC_redist.x86.exe which installs the Microsoft Visual C++ runtime dependencies required by PHP to operate under IIS. It ensures stable and compatible PHP execution for the osTicket application.
</p>
<br />

<p>
  <img src="https://i.imgur.com/TBXJX8X.png" height="80%" width="80%" alt="MySQL Post Install Wizard"/>
  <img src="https://i.imgur.com/mGOk1x0.png" height="80%" width="80%" alt="MySQL Account Setup "/>
  <img src="https://i.imgur.com/zyDxcKV.png" height="80%" width="80%" alt="MySQL server Configuration"/>
</p>
<p>
<strong>Step 5 – Install and Configure MySQL:</strong><br/>
Install MySQL 5.5.62 with standard configuration. Set a username & password then confirm that the MySQL service is running. This database server will store osTicket’s ticketing and user data.
</p>
<br />

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
<p>
<strong>Step 6 – Register PHP within IIS:</strong><br/>
To make the Web Server aware of PHP on the computer. Register PHP from within IIS under Administrator Access. PHP Manager -> <code>C:\PHP\php-cgi.exe</code> After Registering the PHP restart the Server.
</p>
<br />

<p>
  <img src="https://i.imgur.com/olif1kl.png" height="80%" width="80%" alt="Extract osTicket Files"/>

Extract osTicket Files
  
  <img src="https://i.imgur.com/dpaaura.png" height="80%" width="80%" alt="Copy Upload to C Drive inetpub\wwwroot"/>

Copy Upload File to C:\inetpub\wwwroot
  
  <img src="https://i.imgur.com/9EqpCB9.png" height="80%" width="80%" alt="Change name of Folder to osTicket"/>

Change name of folder to osTicket
  
</p>
<p>
<strong>Step 7 – Deploy osTicket Files:</strong><br/>
Copy the “upload” folder from the osTicket installation files to <code>C:\inetpub\wwwroot</code> and rename it to <code>osTicket</code>. Restart IIS and confirm the folder is accessible at <code>http://localhost/osTicket</code>.
</p>
<br />

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="PHP Extensions"/>
</p>
<p>
<strong>Step 8 – Enable PHP Extensions:</strong><br/>
Within PHP Manager, enable <code>php_imap.dll</code>, <code>php_intl.dll</code>, and <code>php_opcache.dll</code>. Restart IIS to apply changes. These extensions are required for email integration, localization, and performance caching.
</p>
<br />

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Database Setup"/>
</p>
<p>
<strong>Step 9 – Create the Database:</strong><br/>
Using HeidiSQL, connect to MySQL with your root credentials. Create a new database named <code>osTicket</code>. This will store all help desk tickets, users, and system settings.
</p
<br />

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="osTicket Installer"/>
</p>
<p>
<strong>Step 10 – Run the osTicket Installer:</strong><br/>
In a browser, navigate to <code>http://localhost/osTicket/setup</code>. Complete the installation by entering your admin details and database credentials (Database: osTicket, User: root, Password: root). Once complete, note your login URL: <code>http://localhost/osTicket/scp/login.php</code>.
</p>
<br />

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Post Install Cleanup"/>
</p>
<p>
<strong>Step 11 – Post-Installation Security:</strong><br/>
Delete the <code>setup</code> folder in the osTicket directory and set <code>ost-config.php</code> to read-only. Log into the admin panel and verify you can create, assign, and resolve tickets.
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
