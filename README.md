<p align="center">
  <img width="415" height="143" alt="image" src="https://github.com/user-attachments/assets/b49951e3-1e1e-405f-8dc8-b27637000c9d" />
  <img width="296" height="64" alt="image" src="https://github.com/user-attachments/assets/43ccd50d-8f73-462d-9cef-53ac9ae102e8" />
</p>

<h1>osTicket Help Desk Ticketing System: Installation, Configuration, and Ticket Lifecycle Management</h1>

<p>
This project demonstrates a complete, end-to-end implementation of the osTicket Help Desk Ticketing System, including installation, configuration, and real-world ticket lifecycle management. The lab begins with deploying a Windows 10 virtual machine in Azure and installing the full osTicket stack, which includes Windows IIS, PHP, MySQL, and required modules, followed by the initial setup of the help desk environment. After installation, we configure core administrative components such as roles, departments, teams, agents, users, SLAs, and help topics to simulate how organizations structure their support workflows. The final section focuses on real operational behavior: creating support tickets as end users, assigning and updating them as help desk agents, applying SLA policies, escalating issues, resolving incidents, and observing how permissions affect visibility and access. Together, these steps provide hands-on experience with a real ticketing system and demonstrate foundational skills for IT, networking, and cybersecurity professionals.
</p>

<p align="center">
  <img width="887" height="413" alt="image" src="https://github.com/user-attachments/assets/501319e6-d24d-4123-b23e-ecdff8b0e76f" />
  <img width="852" height="421" alt="image" src="https://github.com/user-attachments/assets/65028d67-d760-4f43-99d2-4b0e23ceb684" />
  <img width="870" height="503" alt="image" src="https://github.com/user-attachments/assets/fb9fb51d-f0db-4009-8851-72c33fc432e4" />
</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Resource Group, Virtual Network (VNet), Subnet, and a Windows 10 Virtual Machine)
- Remote Desktop (RDP)
- Internet Information Services (IIS)
- PHP Manager for IIS
- IIS URL Rewrite Module 2 (rewrite_amd64_en-US.msi)
- Microsoft Visual C++ Redistributable (VC_redist.x86) (Required for PHP and MySQL)
- MySQL Server 5.5.62 (Database engine used by osTicket)
- HeidiSQL (Database management tool)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)

<h2>High-Level Steps</h2>

- Step 1. Install and Configure osTicket (Server Setup)
- Step 2. Post-Installation Configuration (Help Desk Setup)
- Step 3. Ticket Creation & Ticket Lifecycle Management

<h3>Step 1. Install and Configure osTicket (Server Setup)</h3>

<h4>1. Create a Virtual Machine and a new Resource Group during deployment. Use the settings shown below and choose your own secure password. Click Next, and allow Azure to automatically create a new Virtual Network and Subnet.</h4>

<p>
  <img width="783" height="829" alt="image" src="https://github.com/user-attachments/assets/d75b0b32-0346-4c00-91bf-b98c377d3cd3" />
  <img width="772" height="838" alt="image" src="https://github.com/user-attachments/assets/ed2f1754-34a0-4330-a879-02cfcaccab67" />
  <img width="760" height="808" alt="image" src="https://github.com/user-attachments/assets/ce22ccef-5b24-43e0-bcc9-7309db37657e" />
</p>

<h4>2. Use Remote Desktop (RDP) to connect to your Virtual Machine. Enter the public IP address of the VM along with the username and password you created.</h4>

<p>
  <img width="620" height="388" alt="image" src="https://github.com/user-attachments/assets/b707bff0-503d-4dd4-8665-1504e152d90d" />
</p>

<h4>3. Inside the VM (osticket-vm), download the "osTicket-Installation-Files.zip" file using the following link: https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD and unzip it to the desktop. The extracted folder will be named "osTicket-Installation-Files", and you will use its contents to install osTicket and the required dependencies.</h4>

<p>
  <img width="1137" height="201" alt="image" src="https://github.com/user-attachments/assets/fa3cc8a4-fd0a-4fd7-9f5e-53cd85789342" />
  <img width="630" height="544" alt="image" src="https://github.com/user-attachments/assets/70f1c44b-39ff-45f1-8725-9960ddf705eb" />
  <img width="676" height="240" alt="image" src="https://github.com/user-attachments/assets/e158acfb-b18f-439d-b24c-54cc432250b6" />
</p>

<h4>4. Install Internet Information Services (IIS) and make sure CGI is enabled. To do this, open the Control Panel, select Uninstall a program, then click Turn Windows features on or off. Check the Internet Information Services box, then expand it and go to World Wide Web Services → Application Development Features and check the CGI box and click OK. To verify IIS is installed, open a web browser and go to 127.0.0.1; the default IIS webpage should load.</h4>

<p>
  <img width="625" height="773" alt="image" src="https://github.com/user-attachments/assets/83df2a72-140a-4be5-80f7-25630cf196f8" />
  <img width="923" height="717" alt="image" src="https://github.com/user-attachments/assets/2d5d715a-8abd-4fe3-9716-bf8bd3886782" />
</p>

<h4>5. From the "osTicket-Installation-Files" folder, run and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi).</h4>

<p>
  <img width="805" height="726" alt="image" src="https://github.com/user-attachments/assets/14544eac-1feb-484b-b92b-819fd7994d6a" />
</p>

<h4>6. From the "osTicket-Installation-Files" folder, install the URL Rewrite Module (rewrite_amd64_en-US.msi).</h4>

<p>
  <img width="803" height="720" alt="image" src="https://github.com/user-attachments/assets/04d736c6-3381-45b3-b206-4d254311c147" />
</p>

<h4>7. Create the directory C:\PHP. Then, from the "osTicket-Installation-Files" folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the C:\PHP folder.</h4>

<p>
  <img width="805" height="381" alt="image" src="https://github.com/user-attachments/assets/1672bdd7-cec6-4fc0-94a9-040f4d698f07" />
  <img width="801" height="756" alt="image" src="https://github.com/user-attachments/assets/192393be-619a-440f-a305-5627a00c7e9e" />
  <img width="835" height="936" alt="image" src="https://github.com/user-attachments/assets/ccddbc95-e925-40ae-95bc-c91377da298a" />
</p>

<h4>8. From the "osTicket-Installation-Files" folder, install VC_redist.x86.exe.</h4>

<p>
  <img width="807" height="626" alt="image" src="https://github.com/user-attachments/assets/269dd25b-9dc1-47e3-9e5e-e2e4c532131a" />
</p>

<h4>9. From the "osTicket-Installation-Files" folder, install MySQL 5.5.62 (mysql-5.5.62-win32.msi). Choose Typical Setup, then launch the MySQL Instance Configuration Wizard after installation. Select Standard Configuration and create a MySQL username and password, and complete the MySQL Server installation.</h4>

<p>
  <img width="811" height="692" alt="image" src="https://github.com/user-attachments/assets/f9c44b4f-281b-4a52-a88c-7d95d9eee55a" />
  <img width="802" height="685" alt="image" src="https://github.com/user-attachments/assets/4fb27a57-ccd3-4534-888a-58cd6fbe822e" />
</p>

<h4>10. Open Internet Information Services (IIS) Manager by typing “IIS” in the Windows search bar, right-clicking Internet Information Services (IIS) Manager, and selecting Run as administrator.</h4>

<p>
  <img width="827" height="677" alt="image" src="https://github.com/user-attachments/assets/1848e3af-e63a-4d60-ae25-08027b221215" />
  <img width="957" height="748" alt="image" src="https://github.com/user-attachments/assets/24e57107-a024-4956-b425-e4198ee2e6c1" />
</p>

<h4>11. In IIS, open PHP Manager, then click Register new PHP version. Browse to C:\PHP\php-cgi.exe, select it, and click OK to register PHP.</h4>

<p>
  <img width="951" height="611" alt="image" src="https://github.com/user-attachments/assets/293b7280-f025-479c-99fd-181483afa9d5" />
  <img width="951" height="751" alt="image" src="https://github.com/user-attachments/assets/fd4d58ed-1645-4530-ad42-cafffe5ff12b" />
</p>

<h4>12. Reload IIS (Open IIS as an administrator, then Stop and Start the server to reload IIS).</h4>

<p>
  <img width="795" height="624" alt="image" src="https://github.com/user-attachments/assets/926ab575-1cbc-4d39-b5eb-ae429dc85176" />
  <img width="797" height="624" alt="image" src="https://github.com/user-attachments/assets/dc700cd3-43fe-4070-ad6a-fef4675a7d16" />
</p>

<h4>13. Install osTicket v1.15.8: From the "osTicket-Installation-Files" folder, unzip "osTicket-v1.15.8.zip" and copy the "upload" folder into "C:\inetpub\wwwroot." Inside "C:\inetpub\wwwroot," rename the "upload" folder to "osTicket."</h4>

<p>
  <img width="806" height="765" alt="image" src="https://github.com/user-attachments/assets/61334dc4-0de1-4f55-9238-2d9db31ac847" />
  <img width="813" height="368" alt="image" src="https://github.com/user-attachments/assets/e26434df-9740-4c7d-a222-8e123fe69a07" />
  <img width="811" height="203" alt="image" src="https://github.com/user-attachments/assets/a7ff81ef-437d-45d2-a940-9d0444354cc2" />
</p>

<h4>14. Reload IIS again (Open IIS as an administrator, then Stop and Start the server to reload IIS).</h4>

<p>
  <img width="794" height="622" alt="image" src="https://github.com/user-attachments/assets/7ab2f75f-7ce3-48dc-b53b-b1eec5f347a3" />
  <img width="794" height="623" alt="image" src="https://github.com/user-attachments/assets/e60bd18f-988b-4066-977f-403d40784a7d" />
</p>

<h4>15. </h4>

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h4>Step 1 Summary</h4>

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>

<h3>Step 2. Post-Installation Configuration (Help Desk Setup)</h3>

<h4>1. Lorem</h4>

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h4>Step 2 Summary</h4>

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>

<h3>Step 3. Ticket Creation & Ticket Lifecycle Management</h3>

<h4>1. Lorem</h4>

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h4>Step 3 Summary</h4>

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>

<h2>Conclusion</h2>

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>

<h2>Thank you for checking out my project!</h2>

<p>
If you found it helpful or interesting, subscribe to my YouTube channel and 🔗connect with me on LinkedIn by clicking below:
</p>

[<img align="left" alt="Jeramy | YouTube" width="22px" src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/youtube.svg" />][youtube]
[<img align="left" alt="Jeramy | LinkedIn" width="22px" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" />][linkedin]

<br clear="left"/>

[youtube]: https://youtube.com/@jeramycanals
[linkedin]: https://linkedin.com/in/jeramycanals
