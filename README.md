<p align="center">
  <img width="415" height="143" alt="image" src="https://github.com/user-attachments/assets/b49951e3-1e1e-405f-8dc8-b27637000c9d" />
  <img width="296" height="64" alt="image" src="https://github.com/user-attachments/assets/43ccd50d-8f73-462d-9cef-53ac9ae102e8" />
</p>

<h1>osTicket Help Desk Ticketing System: Installation, Configuration, and Ticket Lifecycle Management</h1>

<p>
This lab demonstrates a complete, end-to-end implementation of the osTicket Help Desk Ticketing System, including installation, configuration, and real-world ticket lifecycle management. The lab begins with deploying a Windows 10 virtual machine in Azure and installing the full osTicket stack, which includes Windows IIS, PHP, MySQL, and required modules, followed by the initial setup of the help desk environment. After installation, we configure core administrative components such as roles, departments, teams, agents, users, SLAs, and help topics to simulate how organizations structure their support workflows. The final section focuses on real operational behavior: creating support tickets as end users, assigning and updating them as help desk agents, applying SLA policies, escalating issues, resolving incidents, and observing how permissions affect visibility and access. Together, these steps provide hands-on experience with a real ticketing system and demonstrate foundational skills for IT, networking, and cybersecurity professionals.
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

<h2>Lab Sections (High-Level Overview)</h2>

<ul>
  <li><a href="#part1">Part 1. Install and Configure osTicket (Server Setup)</a></li>
  <li><a href="#part2">Part 2. Post-Installation Configuration (Help Desk Setup)</a></li>
  <li><a href="#part3">Part 3. Ticket Creation & Ticket Lifecycle Management</a></li>
</ul>

<h3 id="part1">Part 1. Install and Configure osTicket (Server Setup)</h3>

<h4>Step 1. Create a Virtual Machine and a new Resource Group during deployment. Use the settings shown below and choose your own secure password. Click Next, and allow Azure to automatically create a new Virtual Network and Subnet.</h4>

<p>
  <img width="783" height="829" alt="image" src="https://github.com/user-attachments/assets/d75b0b32-0346-4c00-91bf-b98c377d3cd3" />
  <img width="772" height="838" alt="image" src="https://github.com/user-attachments/assets/ed2f1754-34a0-4330-a879-02cfcaccab67" />
  <img width="760" height="808" alt="image" src="https://github.com/user-attachments/assets/ce22ccef-5b24-43e0-bcc9-7309db37657e" />
</p>

<h4>Step 2. Use Remote Desktop (RDP) to connect to your Virtual Machine. Enter the public IP address of the VM along with the username and password you created.</h4>

<p>
  <img width="620" height="388" alt="image" src="https://github.com/user-attachments/assets/b707bff0-503d-4dd4-8665-1504e152d90d" />
</p>

<h4>Step 3. Inside the VM (osticket-vm), download the "osTicket-Installation-Files.zip" file using the following link: https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD and unzip it to the desktop. The extracted folder will be named "osTicket-Installation-Files", and you will use its contents to install osTicket and the required dependencies.</h4>

<p>
  <img width="1137" height="201" alt="image" src="https://github.com/user-attachments/assets/fa3cc8a4-fd0a-4fd7-9f5e-53cd85789342" />
  <img width="630" height="544" alt="image" src="https://github.com/user-attachments/assets/70f1c44b-39ff-45f1-8725-9960ddf705eb" />
  <img width="676" height="240" alt="image" src="https://github.com/user-attachments/assets/e158acfb-b18f-439d-b24c-54cc432250b6" />
</p>

<h4>Step 4. Install Internet Information Services (IIS) and make sure CGI is enabled. To do this, open the Control Panel, select Uninstall a program, then click Turn Windows features on or off. Check the Internet Information Services box, then expand it and go to World Wide Web Services → Application Development Features and check the CGI box and click OK. To verify IIS is installed, open a web browser and go to 127.0.0.1; the default IIS webpage should load.</h4>

<p>
  <img width="625" height="773" alt="image" src="https://github.com/user-attachments/assets/83df2a72-140a-4be5-80f7-25630cf196f8" />
  <img width="923" height="717" alt="image" src="https://github.com/user-attachments/assets/2d5d715a-8abd-4fe3-9716-bf8bd3886782" />
</p>

<h4>Step 5. From the "osTicket-Installation-Files" folder, run and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi).</h4>

<p>
  <img width="805" height="726" alt="image" src="https://github.com/user-attachments/assets/14544eac-1feb-484b-b92b-819fd7994d6a" />
</p>

<h4>Step 6. From the "osTicket-Installation-Files" folder, install the URL Rewrite Module (rewrite_amd64_en-US.msi).</h4>

<p>
  <img width="803" height="720" alt="image" src="https://github.com/user-attachments/assets/04d736c6-3381-45b3-b206-4d254311c147" />
</p>

<h4>Step 7. Create the directory C:\PHP. Then, from the "osTicket-Installation-Files" folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the C:\PHP folder.</h4>

<p>
  <img width="805" height="381" alt="image" src="https://github.com/user-attachments/assets/1672bdd7-cec6-4fc0-94a9-040f4d698f07" />
  <img width="801" height="756" alt="image" src="https://github.com/user-attachments/assets/192393be-619a-440f-a305-5627a00c7e9e" />
  <img width="835" height="936" alt="image" src="https://github.com/user-attachments/assets/ccddbc95-e925-40ae-95bc-c91377da298a" />
</p>

<h4>Step 8. From the "osTicket-Installation-Files" folder, install VC_redist.x86.exe.</h4>

<p>
  <img width="807" height="626" alt="image" src="https://github.com/user-attachments/assets/269dd25b-9dc1-47e3-9e5e-e2e4c532131a" />
</p>

<h4>Step 9. From the "osTicket-Installation-Files" folder, install MySQL 5.5.62 (mysql-5.5.62-win32.msi). Choose Typical Setup, then launch the MySQL Instance Configuration Wizard after installation. Select Standard Configuration and create a MySQL username and password (use "root" for both for lab simplicity), and complete the MySQL Server installation.</h4>

<p>
  <img width="811" height="692" alt="image" src="https://github.com/user-attachments/assets/f9c44b4f-281b-4a52-a88c-7d95d9eee55a" />
  <img width="802" height="685" alt="image" src="https://github.com/user-attachments/assets/4fb27a57-ccd3-4534-888a-58cd6fbe822e" />
</p>

<h4>Step 10. Open Internet Information Services (IIS) Manager by typing “IIS” in the Windows search bar, right-clicking Internet Information Services (IIS) Manager, and selecting Run as administrator.</h4>

<p>
  <img width="827" height="677" alt="image" src="https://github.com/user-attachments/assets/1848e3af-e63a-4d60-ae25-08027b221215" />
  <img width="957" height="748" alt="image" src="https://github.com/user-attachments/assets/24e57107-a024-4956-b425-e4198ee2e6c1" />
</p>

<h4>Step 11. In IIS, open PHP Manager, then click Register new PHP version. Browse to C:\PHP\php-cgi.exe, select it, and click OK to register PHP.</h4>

<p>
  <img width="951" height="611" alt="image" src="https://github.com/user-attachments/assets/293b7280-f025-479c-99fd-181483afa9d5" />
  <img width="951" height="751" alt="image" src="https://github.com/user-attachments/assets/fd4d58ed-1645-4530-ad42-cafffe5ff12b" />
</p>

<h4>Step 12. Reload IIS (Open IIS as an administrator, then Stop and Start the server to reload IIS).</h4>

<p>
  <img width="795" height="624" alt="image" src="https://github.com/user-attachments/assets/926ab575-1cbc-4d39-b5eb-ae429dc85176" />
  <img width="797" height="624" alt="image" src="https://github.com/user-attachments/assets/dc700cd3-43fe-4070-ad6a-fef4675a7d16" />
</p>

<h4>Step 13. Install osTicket v1.15.8: From the "osTicket-Installation-Files" folder, unzip "osTicket-v1.15.8.zip" and copy the "upload" folder into "C:\inetpub\wwwroot." Inside "C:\inetpub\wwwroot," rename the "upload" folder to osTicket.</h4>

<p>
  <img width="806" height="765" alt="image" src="https://github.com/user-attachments/assets/61334dc4-0de1-4f55-9238-2d9db31ac847" />
  <img width="813" height="368" alt="image" src="https://github.com/user-attachments/assets/e26434df-9740-4c7d-a222-8e123fe69a07" />
  <img width="811" height="203" alt="image" src="https://github.com/user-attachments/assets/a7ff81ef-437d-45d2-a940-9d0444354cc2" />
</p>

<h4>Step 14. Reload IIS again (Open IIS as an administrator, then Stop and Start the server to reload IIS).</h4>

<p>
  <img width="794" height="622" alt="image" src="https://github.com/user-attachments/assets/7ab2f75f-7ce3-48dc-b53b-b1eec5f347a3" />
  <img width="794" height="623" alt="image" src="https://github.com/user-attachments/assets/e60bd18f-988b-4066-977f-403d40784a7d" />
</p>

<h4>Step 15. Open the osTicket Site in IIS: In IIS, navigate to Sites → Default Web Site → osTicket. On the right-hand panel, click “Browse *:80” to open the osTicket setup page in your browser.</h4>

<p>
  <img width="639" height="622" alt="image" src="https://github.com/user-attachments/assets/1431a486-fd01-4d16-86ed-5c103af8cb7e" />
  <img width="946" height="878" alt="image" src="https://github.com/user-attachments/assets/6b25d1ef-2bd8-4a01-80bf-5d35aff97902" />
</p>

<h4>Step 16. Enable Required PHP Extensions: When opening the osTicket setup page, you will notice that several PHP extensions are not enabled. To fix this, go back to IIS → Sites → Default Web Site → osTicket, open PHP Manager, and click “Enable or disable an extension.” Enable php_imap.dll, php_intl.dll, and php_opcache.dll, then refresh the osTicket page in your browser to see the changes.</h4>

<p>
  <img width="762" height="743" alt="image" src="https://github.com/user-attachments/assets/1c043fbf-f610-43b1-ac98-482899eb25c4" />
  <img width="764" height="748" alt="image" src="https://github.com/user-attachments/assets/786aae1c-b6cb-4f12-8be1-953ddab48da1" />
  <img width="947" height="885" alt="image" src="https://github.com/user-attachments/assets/3a85f950-cbbe-4e58-a69e-b861a8ebc437" />
</p>

<h4>Step 17. Rename the osTicket Configuration File: Navigate to C:\inetpub\wwwroot\osTicket\include and rename ost-sampleconfig.php to ost-config.php.</h4>

<p>
  <img width="819" height="249" alt="image" src="https://github.com/user-attachments/assets/48667cae-377a-4987-95f1-b0ced3863b60" />
  <img width="823" height="248" alt="image" src="https://github.com/user-attachments/assets/d3f1b7b0-fed3-4871-9358-ca5603676164" />
</p>

<h4>Step 18. Assign Permissions to ost-config.php: Right-click "ost-config.php" and select "Properties," then go to Security → Advanced. Click "Disable inheritance," choose "Remove all inherited permissions from this object." Next, add a new permission entry for Everyone with Full Control by clicking Add → Select a principal, entering "everyone" in the object name field, clicking "Check Names," then clicking OK. In Basic permissions, check Full control, click OK, then click Apply and OK to save the changes.</h4>

<p>
  <img width="1042" height="620" alt="image" src="https://github.com/user-attachments/assets/8945a913-2c93-43a9-a238-f4491323c1c3" />
  <img width="912" height="621" alt="image" src="https://github.com/user-attachments/assets/26739837-ab83-448d-bfc1-8d2cfddc3068" />
  <img width="927" height="719" alt="image" src="https://github.com/user-attachments/assets/ceccdad4-7532-4f46-a655-536492328519" />
  <img width="906" height="584" alt="image" src="https://github.com/user-attachments/assets/22f90c0e-9a60-44c0-bcee-04cf4575b943" />
  <img width="918" height="626" alt="image" src="https://github.com/user-attachments/assets/12c71717-2cad-40e5-91ad-1cbfaf6db683" />
</p>

<h4>Step 19. Click "Continue" to proceed with the osTicket setup in your web browser, and fill out only the "System Settings" and "Admin User" sections with your information. Note: Don't click "Install Now" until you complete Step 21.</h4>

<p>
  <img width="676" height="624" alt="image" src="https://github.com/user-attachments/assets/d5f6c1b9-a0fb-4070-8bce-29b9d482026d" />
  <img width="842" height="809" alt="image" src="https://github.com/user-attachments/assets/2a8be4d1-9ba7-4307-9398-ca1d6eddc5ba" />
  <img width="844" height="487" alt="image" src="https://github.com/user-attachments/assets/ebc9db20-0dd7-494e-a817-8b313e565dd0" />
</p>

<h4>Step 20. From the osTicket-Installation-Files folder, install HeidiSQL, then launch HeidiSQL, and click "Skip" to continue. Click "New" to create a new session, use "root" for both the username and password, and click "Open" to connect to the session. In the left panel, right-click Unnamed → Create new → Database, and name the database osTicket, and click OK.</h4>

<p>
  <img width="944" height="790" alt="image" src="https://github.com/user-attachments/assets/a967c873-74b9-4a1d-b53c-69a210655075" />
  <img width="711" height="493" alt="image" src="https://github.com/user-attachments/assets/587cc1b8-1584-43b7-b68b-5989df44da2a" />
  <img width="703" height="498" alt="image" src="https://github.com/user-attachments/assets/42ef6ce2-a69e-46ba-a386-43323091c673" />
  <img width="994" height="533" alt="image" src="https://github.com/user-attachments/assets/ae5d5c77-f1af-42df-bb9e-5101eb18dad4" />
  <img width="974" height="514" alt="image" src="https://github.com/user-attachments/assets/f81204f3-d820-42c4-868d-882e5e31e7d4" />
</p>

<h4>Step 21. Finish setting up osTicket in your web browser by entering the "MySQL Database" name (osTicket) that you just created.  When prompted for database credentials, use the same MySQL username and password (root) from Step 9, then click Install Now. On the next screen, you should see a "Congratulations!" message, confirming that the osTicket installation was successful. Note: At the bottom of this page, osTicket provides several useful URLs. The osTicket URL (http://localhost/osTicket/) is the end-user portal where customers submit and view tickets. The Staff Control Panel (http://localhost/osTicket/scp) is the administrative dashboard where help desk admins and agents manage and respond to tickets. The osTicket Forums (https://forum.osticket.com/) offer community support, troubleshooting discussions, and guidance from other users. Finally, the osTicket Documentation (https://docs.osticket.com/) provides official setup instructions, configuration details, and advanced administrative guidance.</h4>

<p>
  <img width="996" height="526" alt="image" src="https://github.com/user-attachments/assets/764de77a-4ab1-4b85-9084-77ad54639e09" />
  <img width="841" height="673" alt="image" src="https://github.com/user-attachments/assets/44ccddbf-d609-4d8c-ba14-049d1fa28a9e" />
</p>

<h4>Step 22. Log In as an Admin and view the End-User Portal: Log in to the Staff Control Panel (http://localhost/osTicket/scp/login.php) using the Admin User credentials you created earlier to access the administrative dashboard, where help desk agents manage and respond to tickets. Then, open the End-User Portal (http://localhost/osTicket/) to view the interface where end-users submit and track support tickets. Verifying access to both interfaces ensures that the osTicket installation is functioning correctly for administrators and end-users. We will use these URLs in Parts 2 and 3 of the lab.</h4>

<p>
  <img width="675" height="607" alt="image" src="https://github.com/user-attachments/assets/ebab4a3e-b5fb-4b11-802d-90caf0918142" />
  <img width="1001" height="458" alt="image" src="https://github.com/user-attachments/assets/d0a6b8b6-8292-4869-b4bb-26e8cac1cd7b" />
  <img width="1003" height="629" alt="image" src="https://github.com/user-attachments/assets/aad6b2b0-a3aa-4ddd-a362-42e3044a02d3" />
</p>

<h4>Step 23. Clean Up the Installation: Delete the C:\inetpub\wwwroot\osTicket\setup folder, then set the permissions on C:\inetpub\wwwroot\osTicket\include\ost-config.php to Read only. To do this, navigate to the file, right-click ost-config.php, select Properties, and at the bottom of the General tab, check the box labeled Read-only. Click Apply, then OK. Note: Make sure to complete this step to prevent warning messages when launching osTicket.</h4>

<p>
  <img width="820" height="480" alt="image" src="https://github.com/user-attachments/assets/97f5d316-f559-45c8-b42d-bf0652c7d21a" />
  <img width="824" height="485" alt="image" src="https://github.com/user-attachments/assets/f9c04d89-0c3c-42cd-a99c-6d1f311c7ecf" />
  <img width="829" height="489" alt="image" src="https://github.com/user-attachments/assets/5a74666a-b699-4c9a-b206-6a7554808939" />
  <img width="819" height="898" alt="image" src="https://github.com/user-attachments/assets/3dd26e36-e9f9-402b-95c6-136ae7240f7a" />
</p>

<h4>Part 1 Summary</h4>

<p>
Part 1 of this lab walks through building the complete osTicket server environment from the ground up, beginning with the creation of a new Resource Group, Virtual Network, and Subnet in Microsoft Azure while deploying a Windows 10 virtual machine. After connecting to the VM via Remote Desktop, we download the osTicket installation bundle and configure the web server environment by installing Internet Information Services (IIS) with CGI support, PHP Manager for IIS, and the IIS URL Rewrite Module 2. Next, we create the C:\PHP directory and extract PHP 7.3.8 into this folder, followed by installing the Microsoft Visual C++ Redistributable and MySQL 5.5.62. We then register PHP within IIS using PHP Manager and verify IIS functionality before deploying the osTicket application by copying the upload folder into C:\inetpub\wwwroot and renaming it to osTicket. After that, we enable essential PHP extensions, rename ost-sampleconfig.php to ost-config.php, and assign the required file permissions. Using HeidiSQL, we create the osTicket MySQL database and complete the web-based installer, confirming success with the “Congratulations!” page. Finally, we verify access to both the Staff Control Panel and End-User Portal, then clean up by deleting the setup folder and setting ost-config.php to read-only. By the end of Part 1, the full backend infrastructure for osTicket is deployed, secured, and fully operational, ready for setup and customization in Part 2.
</p>

<h3 id="part2">Part 2. Post-Installation Configuration (Help Desk Setup)</h3>

<h4>Step 24. Acknowledge Agent Panel vs Admin Panel: Log in to the Staff Control Panel at http://localhost/osTicket/scp/login.php using your admin credentials. After signing in, you will initially land in the Agent Panel, where help desk agents manage and respond to tickets. To switch to full administrative privileges, click “Admin Panel” in the top-right corner. This opens the Admin Panel, where administrators configure roles, departments, teams, SLAs, help topics, and system-wide settings.</h4>

<p>
  <img width="1314" height="620" alt="image" src="https://github.com/user-attachments/assets/97adfdbe-ebcd-4ca9-91fa-9495dc914cba" />
  <img width="1157" height="732" alt="image" src="https://github.com/user-attachments/assets/863b52ed-313d-4e22-a15e-da1d47f41914" />
</p>

<h4>Step 25. Roles Overview: In the Admin Panel, go to Agents → Roles (make sure you clicked the “Agents” button near the top-right corner). The Roles page displays all permission groups that determine what agents are allowed to do within osTicket. Here you will see options to create new roles or edit existing ones, and each role can be assigned specific permissions such as viewing tickets, editing tickets, managing users, or accessing advanced administrative functions. This is where you define permission sets that agents can inherit based on their responsibilities. Click Expanded Access → Permissions to view the specific permissions assigned to the default Expanded Access role.</h4>

<p>
  <img width="1106" height="507" alt="image" src="https://github.com/user-attachments/assets/00f56e2d-00b2-4d9e-b6d9-1c4d9bb49534" />
  <img width="1104" height="823" alt="image" src="https://github.com/user-attachments/assets/e29ac729-7f5d-43a3-bd27-2a1c16a3b975" />
  <img width="1018" height="673" alt="image" src="https://github.com/user-attachments/assets/15311d80-caf9-49db-a074-1e42c3fb4b9d" />
  <img width="1013" height="527" alt="image" src="https://github.com/user-attachments/assets/ea755f09-44a3-4295-8d5c-01fbabd243df" />
</p>

<h4>Step 26. Create a new Role:  In the Admin Panel, go to Agents → Roles → Add New Role. Name the role “Supreme Admin”, then open the Permissions tab. Under Tickets, check every permission box to grant full ticket management capabilities. Next, click Tasks and check every box to enable full task-related permissions. Then click Knowledgebase and check its available permission as well. Once all permissions are selected, click "Add Role" to create the new Supreme Admin role.</h4>

<p>
  <img width="1109" height="687" alt="image" src="https://github.com/user-attachments/assets/a74ef049-7096-4673-82b1-a8ed95fbe6fa" />
  <img width="1097" height="841" alt="image" src="https://github.com/user-attachments/assets/6a9a30d7-25a6-484a-ac85-972788f22937" />
  <img width="1098" height="674" alt="image" src="https://github.com/user-attachments/assets/92fc3547-8c64-4b79-8a3d-965bfbce54cf" />
  <img width="1100" height="525" alt="image" src="https://github.com/user-attachments/assets/019e359c-3a38-417c-8360-94f9312a9c46" />
  <img width="1103" height="560" alt="image" src="https://github.com/user-attachments/assets/695f8d94-290f-433e-85ee-ea3929470d79" />
</p>

<h4>Step 27. Configure Departments: In the Admin Panel, navigate to Agents → Departments → Add New Department. Set the Parent department to Top-Level Department, then name the new department SysAdmins. Once completed, click Create Dept to add the department.</h4>

<p>
  <img width="792" height="936" alt="image" src="https://github.com/user-attachments/assets/e9396a88-d87f-4d64-ac2c-4a4b07835ac9" />
  <img width="1107" height="498" alt="image" src="https://github.com/user-attachments/assets/6dddf9b9-2cf9-47f2-922e-1601c8f962cb" />
</p>

<h4>Step 28. Configure Teams: In the Admin Panel, navigate to Agents → Teams → Add New Team. Teams allow you to group agents from different departments. Name the team “Online Banking”, then click "Create Team" to add it.</h4>

<p>
  <img width="1013" height="421" alt="image" src="https://github.com/user-attachments/assets/32ab8861-d3d9-412c-a632-c681d8f2c20d" />
  <img width="826" height="638" alt="image" src="https://github.com/user-attachments/assets/9f3e4c9b-73c7-47bd-9858-152535064cfd" />
  <img width="1019" height="823" alt="image" src="https://github.com/user-attachments/assets/8566b416-bd65-4e09-833d-aaca1b91a091" />
  <img width="1015" height="456" alt="image" src="https://github.com/user-attachments/assets/a3fd2bcd-8104-42b7-aacd-7918a08bec13" />
</p>

<h4>Step 29. In the Admin Panel, go to Settings → Users and make sure the option “Require registration and login to create tickets” is unchecked. This allows unregistered users to submit tickets through the End-User Portal, and make sure to save any changes.</h4>

<p>
  <img width="952" height="798" alt="image" src="https://github.com/user-attachments/assets/e93db7bd-7f47-48fb-955f-fdc60ea53139" />
</p>

<h4>Step 30. Configure Agents (workers): In the Admin Panel, go to Agents → Add New Agent. Create a new agent named “Jane Doe,” then enter her email address and username. Click "Set Password", uncheck "Send the agent a password reset email", fill out the password fields, and uncheck "Require password change at next login" for lab simplicity. Click "Update" to set the agent's password.  Under Access, set her Primary Department to "SysAdmins" and assign her the "Supreme Admin" role. In the Teams section, select the "Online Banking" team and click "Add". Click "Create" to add the agent. Next, return to Agents → Add New Agent and create another agent named "John Doe". Enter his email address and username, then click "Set Password". Uncheck "Send the agent a password reset email", fill out the password fields, and uncheck "Require password change at next login". Click "Update" to set the agent's password. Under Access, set his Primary Department to "Support" and assign the "All Access" role. In the Teams section, select the "Level I Support" team and click "Add".  Click "Create" to add the agent.</h4>

<p>
  <img width="943" height="470" alt="image" src="https://github.com/user-attachments/assets/e4aaf398-087f-4a40-963b-1b4fcdac6584" />
  <img width="975" height="1010" alt="image" src="https://github.com/user-attachments/assets/b9d326e5-ccdd-4792-898c-6b9c460d0f69" />
  <img width="967" height="618" alt="image" src="https://github.com/user-attachments/assets/2ee9f664-c6f7-413e-b2a1-fd11eac27c6b" />
  <img width="968" height="658" alt="image" src="https://github.com/user-attachments/assets/9776fee8-2f2e-42d3-bde5-e947bad7ff42" />
  <img width="968" height="609" alt="image" src="https://github.com/user-attachments/assets/d65bf82d-9dd2-4396-886b-c41edffd6f25" />
  <img width="976" height="476" alt="image" src="https://github.com/user-attachments/assets/6b66a0e5-7507-4f74-9302-659796b16b27" />
  <img width="968" height="1005" alt="image" src="https://github.com/user-attachments/assets/7261e1f6-5749-441a-b0c5-e33a8512f778" />
  <img width="969" height="621" alt="image" src="https://github.com/user-attachments/assets/2f0eb6f4-c48b-423d-898a-1370c8930a43" />
  <img width="952" height="648" alt="image" src="https://github.com/user-attachments/assets/a163411a-c279-45d1-aad7-df7f4e0bf060" />
  <img width="1097" height="604" alt="image" src="https://github.com/user-attachments/assets/60e19b1d-44cf-4ca1-99a7-20f71809d757" />
  <img width="967" height="516" alt="image" src="https://github.com/user-attachments/assets/39577dcc-6593-482b-bc23-6fb4ea9b739f" />
</p>

<h4>Step 31. Configure Users (customers): In the Agent Panel, go to Users → Add User. Create a user named “Karen Doe”, then enter her email address and click "Add User" to add the customer account. Next, return to Users → Add User and create another user named "Ken Doe". Enter his email address and click "Add User" to complete the creation of the second customer.</h4>

<p>
  <img width="969" height="452" alt="image" src="https://github.com/user-attachments/assets/2bfce7b3-bd28-45ec-a7c9-33b2679b1771" />
  <img width="968" height="631" alt="image" src="https://github.com/user-attachments/assets/26f8c9a6-62df-432a-a000-478d3f2044d0" />
  <img width="970" height="511" alt="image" src="https://github.com/user-attachments/assets/69a7af49-6c11-457b-b042-8cb1bf5e2813" />
  <img width="971" height="486" alt="image" src="https://github.com/user-attachments/assets/4d1bcbca-7009-47a7-b08c-bba8ac8bb209" />
  <img width="966" height="632" alt="image" src="https://github.com/user-attachments/assets/9f7befe4-e8d8-47f5-8a3a-05341fb80291" />
  <img width="970" height="520" alt="image" src="https://github.com/user-attachments/assets/28e2c11f-6a38-4d6f-9410-54a01c2c902a" />
  <img width="971" height="519" alt="image" src="https://github.com/user-attachments/assets/c471c5f0-0ead-4330-98fc-2d52be29d96a" />
</p>

<h4>Step 32. Configure SLA: In the Admin Panel, go to Manage → SLA → Add New SLA Plan. Create a new SLA named "Sev-A", set the Grace Period to 1 hour, and set the Schedule to 24/7. Click "Add Plan" to create the SLA. Next, return to Manage → SLA → Add New SLA Plan and create a second SLA named "Sev-B". Set the Grace Period to 4 hours and the Schedule to 24/7, then click "Add Plan". Finally, return once more to Manage → SLA → Add New SLA Plan and create a third SLA named "Sev-C". Set the Grace Period to 8 hours and the Schedule to "Monday - Friday 8am - 5pm with U.S. Holidays". Click "Add Plan" to create the SLA.</h4>

<p>
  <img width="974" height="412" alt="image" src="https://github.com/user-attachments/assets/ab36628b-9c89-457d-8dd7-0e5019de3851" />
  <img width="968" height="768" alt="image" src="https://github.com/user-attachments/assets/4ed6a772-56d8-405e-bd47-ea9a58393d5d" />
  <img width="972" height="484" alt="image" src="https://github.com/user-attachments/assets/b0975fec-8e3a-4925-8e71-912da142104b" />
  <img width="971" height="774" alt="image" src="https://github.com/user-attachments/assets/a583c582-095e-45ba-bb5b-14c157401494" />
  <img width="963" height="506" alt="image" src="https://github.com/user-attachments/assets/800c0d52-b418-4907-aaee-109177784bf4" />
  <img width="952" height="777" alt="image" src="https://github.com/user-attachments/assets/d99773ce-2721-4dd6-949d-9e0d3dee9d56" />
  <img width="954" height="533" alt="image" src="https://github.com/user-attachments/assets/969ff2d5-e231-4017-86ac-db68be462b55" />
</p>

<h4>Step 33. Configure Help Topics (Used  When Users Create Tickets): In the Admin Panel, go to Manage → Help Topics → Add New Help Topic. Create a new Help Topic named "Business Critical Outage" and set the Parent Topic to "Report a Problem". Click "Add Topic" to create the Help Topic. This determines how ticket categories are organized when end-users submit new tickets. Next, return to Manage → Help Topics → Add New Help Topic and create a second Help Topic named "Personal Computer Issues". Set the Parent Topic to "Report a Problem", then click "Add Topic" to create the Help Topic. Then, go again to Manage → Help Topics → Add New Help Topic and create a third Help Topic named "Equipment Request". Set the Parent Topic to "General Inquiry", and click "Add Topic" to create the Help Topic. Repeat the process to create a fourth Help Topic named "Password Reset". Set the Parent Topic to "Report a Problem," and click Add Topic to create the Help Topic. Finally, create a fifth Help Topic named “Other.” Set the Parent Topic to “General Inquiry,” and click "Add Topic" to complete the Help Topic configuration.</h4>

<p>
  <img width="953" height="533" alt="image" src="https://github.com/user-attachments/assets/ec890d75-cc00-490d-a3ac-f9775bef26f5" />
  <img width="956" height="744" alt="image" src="https://github.com/user-attachments/assets/295eda5a-35e0-4b98-a1c8-4b8c62a18ddd" />
  <img width="945" height="593" alt="image" src="https://github.com/user-attachments/assets/40e9fc80-f615-4301-97c5-d38419dd5b92" />
  <img width="813" height="635" alt="image" src="https://github.com/user-attachments/assets/9b73cdda-ca4b-498b-a541-9db033eb2cae" />
  <img width="950" height="652" alt="image" src="https://github.com/user-attachments/assets/17f37c6b-e318-4b95-8eea-37d71ea1c5df" />
  <img width="953" height="740" alt="image" src="https://github.com/user-attachments/assets/af5222b2-01d2-45f1-8683-b1fe6538ef27" />
  <img width="952" height="710" alt="image" src="https://github.com/user-attachments/assets/2c12443d-7f6b-4f81-b859-e2a26a6d0fd9" />
  <img width="957" height="748" alt="image" src="https://github.com/user-attachments/assets/ab8886f2-33ce-4fc8-91d7-846683dfac5a" />
  <img width="952" height="729" alt="image" src="https://github.com/user-attachments/assets/004d4223-3eae-436b-abf3-de5c6ff9ec4a" />
  <img width="958" height="741" alt="image" src="https://github.com/user-attachments/assets/0b03d6f7-6d09-4109-9fc9-c50391aaa4af" />
  <img width="951" height="770" alt="image" src="https://github.com/user-attachments/assets/953d5fda-5712-4af3-bfd4-97b3d4e4082b" />
</p>

<h4>Step 34. Delete the Maintenance Department: To prevent tickets from being automatically assigned to the Maintenance department, go to the Admin Panel → Agents → Departments. Check the box next to “Maintenance,” click More, and select Delete. When the confirmation pop-up appears, click “Yes, Do it” to remove the department.</h4>

<p>
  <img width="953" height="474" alt="image" src="https://github.com/user-attachments/assets/01fd374d-f276-444d-a74e-33aa95ab1c90" />
  <img width="949" height="536" alt="image" src="https://github.com/user-attachments/assets/3c2564aa-0993-42a7-895c-9d59f192b7ee" />
  <img width="954" height="481" alt="image" src="https://github.com/user-attachments/assets/bec1033e-fca8-4bd6-8798-ee119acb9890" />
</p>

<h4>Part 2 Summary</h4>

<p>
In Part 2, we configured the core administrative structure that powers the osTicket help desk environment. We began by distinguishing the Agent Panel from the Admin Panel, then created custom roles, departments, and teams to define how permissions and responsibilities are organized. We enabled ticket submission for unregistered users and added two example agents with different permission levels to demonstrate access control. Next, we created customer accounts for end users and configured three SLA plans (Sev-A, Sev-B, and Sev-C) to define response expectations and scheduling rules. We also built out five Help Topics that categorize incoming tickets, ensuring that issues are routed properly based on their type.  Finally, we cleaned up the default configuration by deleting the unused Maintenance department to prevent tickets from being automatically assigned there. Together, these steps established the full administrative foundation required for realistic ticket handling in the next section of the lab.
</p>

<h3 id="part3">Part 3. Ticket Creation & Ticket Lifecycle Management</h3>



<h4>Step 35. Creating a Ticket as an End-User (Karen): Go to the End-User Portal URL (http://localhost/osTicket) and click "Open a New Ticket". Using the customer account you created earlier, fill out the form as Karen Doe. Enter her Email Address, Full Name, and Phone Number. For the Help Topic, select "Report a Problem". In the Issue Summary, enter "entire mobile/online banking system is down". In the details box, type the following description: "My employees are reporting that users are no longer able to access the online banking portal. The ones who can occasionally access it cannot log in." Once all fields are completed, click "Create Ticket" to submit the issue.</h4>

<p>
  <img width="957" height="625" alt="image" src="https://github.com/user-attachments/assets/6e4b3687-a19a-4564-9cc4-47cef8b7f81c" />
  <img width="949" height="946" alt="image" src="https://github.com/user-attachments/assets/7f31ab5d-84e5-4aea-9613-11e1fa140a14" />
  <img width="958" height="569" alt="image" src="https://github.com/user-attachments/assets/720c73d5-8a3e-4bc1-bcb7-462b3d2b7c5e" />
</p>

<h4>Step 36. Log In and View the Ticket's Properties as Help Desk Agent (John): Go to the Staff Control Panel at "http://localhost/osTicket/scp/login.php"
 and log in as John, the Help Desk Agent you created earlier in the lab. After signing in, open the Tickets tab and locate the ticket submitted by Karen Doe. Click the ticket number to open it and review all of the ticket's properties, such as Priority, Department, SLA Plan, and Assigned To, from the help desk agent’s perspective.</h4>

<p>
  <img width="953" height="525" alt="image" src="https://github.com/user-attachments/assets/2f2a09da-5fb2-47f5-96b8-be5ba8414fd1" />
  <img width="949" height="440" alt="image" src="https://github.com/user-attachments/assets/5cca2597-da6a-4606-844c-d39c3b0209e0" />
  <img width="955" height="945" alt="image" src="https://github.com/user-attachments/assets/b3879eff-881a-471e-94d4-71b2dbd39f53" />
</p>

<h4>Step 37. Update the Ticket's SLA Plan (John): In the ticket view, locate the SLA Plan field, click on "Default SLA", and change the SLA Plan to Sev-A, since this is a major, high-impact issue that requires immediate and continuous attention. In the Reason for Update box, enter: "This issue has a wide impact; customers are unable to access online banking". Then click Update to apply the changes.</h4>

<p>
  <img width="1422" height="750" alt="image" src="https://github.com/user-attachments/assets/2ab0451b-7266-4926-86a6-5c80eb416279" />
  <img width="951" height="493" alt="image" src="https://github.com/user-attachments/assets/11a81505-699e-444b-a902-d230f14c1498" />
  <img width="986" height="759" alt="image" src="https://github.com/user-attachments/assets/fff6fc06-b2b1-4937-a4c5-d436105b7e3d" />
</p>

<h4>Step 38. Update the Ticket's Help Topic (John): In the ticket view, locate the Help Topic field, click "Report a Problem" and change the Help Topic to "Report a Problem / Business Critical Outage" since it is more appropriate for the severity of the issue. In the Reason for Update box, enter: "No customers are able to access online banking." Then click Update to apply the changes.</h4>

<p>
  <img width="983" height="766" alt="image" src="https://github.com/user-attachments/assets/64d0b823-77c6-477c-84a4-cdb6a541e07b" />
  <img width="1106" height="485" alt="image" src="https://github.com/user-attachments/assets/25ff6152-e5b0-45fe-973b-41ffa0331ba1" />
  <img width="1107" height="947" alt="image" src="https://github.com/user-attachments/assets/99b84d90-91aa-47b5-842e-d8e5d94b483f" />
</p>

<h4>Step 39. Update the Ticket's Assigned To (John): In the ticket view, locate the Assigned To field, click "— Unassigned —" and change the Assignee to the Online Banking team. In the Reason for Update box, enter: "Customers are not able to access the online banking portal, assigning to the online banking team." Then click Assign to apply the changes.</h4>

<p>
  <img width="1098" height="956" alt="image" src="https://github.com/user-attachments/assets/4ccd1fba-c4ac-42e3-b081-eb0a5d950223" />
  <img width="644" height="199" alt="image" src="https://github.com/user-attachments/assets/5475d548-5f52-412c-8f00-bff1e92ae02a" />
  <img width="645" height="861" alt="image" src="https://github.com/user-attachments/assets/4cd860e9-bcfe-4801-8292-fd087c604265" />
</p>

<h4>Step 40. Log In and Open the Ticket (Jane): Log out of John’s account, then log back in as Jane, the Supreme Admin you created earlier in the lab. After signing in, locate the “entire mobile/online banking system is down” ticket and click the ticket number to open it.</h4>

<p>
  <img width="1105" height="565" alt="image" src="https://github.com/user-attachments/assets/2cc0097f-ff7f-46f6-8c2a-369b9a26275c" />
  <img width="1105" height="473" alt="image" src="https://github.com/user-attachments/assets/6a810a57-abbf-4d85-b9d6-89fba48c127f" />
  <img width="1098" height="964" alt="image" src="https://github.com/user-attachments/assets/701b7842-743b-4e42-b08e-b19ad8dfe27d" />
</p>

<h4>Step 41. Start Working the Ticket, Update the Ticket's Assigned To (Jane): In the ticket view, locate the Assigned To field. Click "Online Banking" and change the Assignee to "Jane Doe" so she can take direct ownership of the ticket. In the Reason for Update box, enter: "I'll be taking this ticket." Then click Assign to apply the changes.</h4>

<p>
  <img width="1107" height="494" alt="image" src="https://github.com/user-attachments/assets/2db23f43-4958-41b0-8afc-59c1d7d6aa74" />
  <img width="1106" height="517" alt="image" src="https://github.com/user-attachments/assets/d3db47be-f963-4189-aacb-a8c10466019c" />
  <img width="637" height="885" alt="image" src="https://github.com/user-attachments/assets/c471b20b-25f9-4aaa-8d05-9a9accefd0e7" />
</p>

<h4>Step 42. Post an Update Reply (Jane):  In the ticket view, scroll down to the Post Reply box, and in the text field, enter: “I suspect the problem might be related to the recent updates. We tested them sufficiently, but I am going to look into it further and roll them back if I determine that was the cause.” Then click Post Reply to add the update to the ticket.</h4>

<p>
  <img width="1185" height="963" alt="image" src="https://github.com/user-attachments/assets/b1d8b9be-20fd-412f-a8f4-ff64f1b604b9" />
  <img width="1199" height="282" alt="image" src="https://github.com/user-attachments/assets/656e6559-3028-4416-a6b7-851fa80c298a" />
</p>

<h4>Step 43. Simulate the Issue Being Fixed and Post Another Update (Jane): We will now pretend the issue has been resolved and add another update to the ticket. In the ticket view, scroll down to the Post Reply box and enter: “It was determined that the root cause was the recent update. We rolled it back, notified the vendor, and are waiting for a proper fix. Online banking should now be up and running.” Then click Post Reply to add the update to the ticket.</h4>

<p>
  <img width="1204" height="987" alt="image" src="https://github.com/user-attachments/assets/df334a89-904f-4601-8b2f-8519f49bc753" />
  <img width="1199" height="981" alt="image" src="https://github.com/user-attachments/assets/473da6ee-a3a9-445e-950f-acaf7775614d" />
</p>

<h4>Step 44. Resolve the ticket (Jane): Scroll to the top of the ticket view and locate the Status field. Click “Open,” then select “Resolved.” A pop-up window will appear. Update the ticket status to Resolved, and in the Reason for Status Change box, enter: “Issue resolved after rolling back the recent update. Online banking is now fully operational.” Then click Close to apply the changes and mark the issue as completed. Once resolved, the ticket will disappear from the Open Tickets tab, confirming that it has been successfully closed.</h4>

<p>
  <img width="1208" height="590" alt="image" src="https://github.com/user-attachments/assets/ab9b5c2d-02d5-45a0-aa16-858fb262bb68" />
  <img width="1168" height="594" alt="image" src="https://github.com/user-attachments/assets/0d711d6f-67a7-4ec8-870a-7cebe9e81926" />
  <img width="576" height="162" alt="image" src="https://github.com/user-attachments/assets/3aea86f6-a2c9-421e-af18-85deb625ea21" />
  <img width="1198" height="382" alt="image" src="https://github.com/user-attachments/assets/8602db80-fbfa-443a-ba70-55a4b1eb4727" />
</p>

<h4>Step 45. Creating a Ticket as an End-User (Ken): Go to the End-User Portal URL (http://localhost/osTicket) and click "Open a New Ticket". Using the customer account you created earlier, fill out the form as Ken Doe. Enter his Email Address, Full Name, and Phone Number. For the Help Topic, select "General Inquiry / Other". In the Issue Summary, enter "accounting department needs adobe upgrade, broken". Then, in the details box, type the following description: "It looks like many people in the accounting department can't use their adobe software." After completing all fields, click "Create Ticket" to submit the issue.</h4>

<p>
  <img width="1133" height="533" alt="image" src="https://github.com/user-attachments/assets/77c6c0e7-a085-4f7f-8e33-3ee9381a249f" />
  <img width="1184" height="978" alt="image" src="https://github.com/user-attachments/assets/b5a3a8cf-0d9e-4aea-a4b5-3db9c7c1bbdf" />
  <img width="1176" height="566" alt="image" src="https://github.com/user-attachments/assets/933b9494-409d-4051-abd3-fe05e5b05100" />
</p>

<h4>Step 46. Log In and Open the Ticket (John): Go to the Staff Control Panel login page (http://localhost/osTicket/scp/login.php) and log in as John. After signing in, open the Tickets tab and locate the ticket titled “accounting department needs adobe upgrade, broken.” Click the ticket number to open it and view the issue details from the agent’s perspective.</h4>

<p>
  <img width="1206" height="525" alt="image" src="https://github.com/user-attachments/assets/afe1ac89-f81a-4f17-8dbc-412618022a82" />
  <img width="1201" height="438" alt="image" src="https://github.com/user-attachments/assets/6d830b9b-9f90-4c28-a17d-b8fda725d576" />
  <img width="1175" height="622" alt="image" src="https://github.com/user-attachments/assets/2617b9a0-d0b5-40e4-92bf-8e697cb7f5ca" />
</p>

<h4>Step 47. Update the Ticket's SLA Plan After Simulating Additional Information (John): In the ticket view, locate the SLA Plan field, click “Default SLA,” and change the SLA Plan to Sev-C, since the follow-up details from the end user indicate that only two employees are affected. In the Reason for Update box, enter: "Only two users are unable to open Adobe Reader, classifying as Sev-C." Then click Update to apply the changes.</h4>

<p>
  <img width="1175" height="622" alt="image" src="https://github.com/user-attachments/assets/43ce10e1-609e-4a98-aadb-87d95efdbf48" />
  <img width="1033" height="614" alt="image" src="https://github.com/user-attachments/assets/b3b076ea-ee9d-4d37-ba95-e0b075e758f3" />
  <img width="1037" height="658" alt="image" src="https://github.com/user-attachments/assets/ab81c04a-0620-4bd6-9122-f659e79a6d8c" />
</p>

<h4>Step 48. Update the Accounting Ticket's Assigned To (John): In the ticket view, locate the Assigned To field, click “— Unassigned —”, and change the Assignee to John Doe so he can begin working on the issue. In the Reason for Update box, enter: "Taking ownership of this ticket." Then click Assign to apply the changes.</h4>

<p>
  <img width="1034" height="662" alt="image" src="https://github.com/user-attachments/assets/02f5808a-3d82-42d1-9fdc-173f0b6b9dfc" />
  <img width="1036" height="649" alt="image" src="https://github.com/user-attachments/assets/73b193de-f8ab-46e2-9aca-037f6c5a698a" />
  <img width="1204" height="653" alt="image" src="https://github.com/user-attachments/assets/51536a89-79c8-410c-b186-86024a0d0b13" />
</p>

<h4>Step 49. Post an Update Reply (John): In the ticket view, scroll down to the Post Reply box. In the text field, enter: “Customer reports that only two users in the accounting department are unable to open or use Adobe Reader. Customer is testing a system restart and will follow up after lunch.” Then click Post Reply to add the update to the ticket.</h4>

<p>
  <img width="1040" height="968" alt="image" src="https://github.com/user-attachments/assets/5a3e0865-443c-4272-96b2-2c52c80f4bfc" />
  <img width="1066" height="979" alt="image" src="https://github.com/user-attachments/assets/711b7145-bb5b-462b-b662-daeed05e90cb" />
</p>

<h4>Step 50. Post an Update Reply After Simulating Additional Information (John): In the ticket view, scroll down to the Post Reply box. In the text field, enter: “Customer reports that a restart resolved the issue. Closing out the ticket.” Then click Post Reply to add the update to the ticket.</h4>

<p>
  <img width="1040" height="980" alt="image" src="https://github.com/user-attachments/assets/88d26406-5a0f-4fbb-beb0-8086ba7c1522" />
  <img width="1042" height="975" alt="image" src="https://github.com/user-attachments/assets/f3b96475-21bc-4763-9679-14344c6f7e7c" />
</p>

<h4>Step 51. Post an Internal Note (John): In the ticket view, scroll down and select the Post Internal Note tab. In the text field, enter: “Customer is upset, make sure to remain empathetic during future communication.” Then click Post Note to add the internal update to the ticket. Note: Always write internal notes as if the customer might see them. Even though internal notes are not shown to end-users, it’s best practice to keep them professional in case they are ever exposed.</h4>

<p>
  <img width="1056" height="968" alt="image" src="https://github.com/user-attachments/assets/668193db-8ec9-4f2b-b967-d66260571d2c" />
  <img width="1028" height="969" alt="image" src="https://github.com/user-attachments/assets/9d6a07db-b3da-479e-abe5-080f3a37ae2b" />
  <img width="1030" height="976" alt="image" src="https://github.com/user-attachments/assets/d8edd464-be33-40cb-8356-765872eb9759" />
</p>

<h4>Step 52. Update the Internal Note Title (John): In the ticket view, scroll down to the Internal Note you just created. Click the small down arrow next to it and select Edit. In the Title field, enter: “Customer is upset.” Then click Save to update the internal note.</h4>

<p>
  <img width="1195" height="566" alt="image" src="https://github.com/user-attachments/assets/e3fe65ec-68e3-4b7b-8525-e303f1ffa6ea" />
  <img width="939" height="562" alt="image" src="https://github.com/user-attachments/assets/eb1e1260-75d2-4a37-b190-59d1bd43cbb3" />
  <img width="1052" height="596" alt="image" src="https://github.com/user-attachments/assets/6240c319-2731-4e36-be2f-53699d3d0f6a" />
</p>

<h4>Step 53. Resolve the Ticket (John): Scroll to the top of the ticket view and locate the Status field. Click “Open,” then select “Resolved.” A pop-up window will appear. Update the ticket status to Resolved, and in the Reason for Status Change box, enter: “Restart fixed the issue for both users.” Then click Close to apply the changes and mark the issue as completed. Once resolved, the ticket will disappear from the Open Tickets tab, confirming that it has been successfully closed.</h4>

<p>
  <img width="1090" height="652" alt="image" src="https://github.com/user-attachments/assets/9dc4bb9f-04cd-464c-b156-40a212437aee" />
  <img width="1031" height="616" alt="image" src="https://github.com/user-attachments/assets/3586edc9-3f6b-42ac-b399-8c1ca175f69a" />
  <img width="1043" height="425" alt="image" src="https://github.com/user-attachments/assets/f3abd40a-2aeb-40e7-9ea4-41ec845f8eec" />
  <img width="1036" height="404" alt="image" src="https://github.com/user-attachments/assets/02dda139-9e81-4548-ad0a-e3e9f4a319bf" />
</p>


<h4>Step 54. View Closed Tickets (John): Go to the Tickets tab, then click the Closed filter to view all resolved tickets. This page displays useful information such as the ticket number, date closed, subject, the user who created the ticket, and the agent who closed it. Viewing closed tickets helps verify successful resolutions and provides a historical record for auditing or follow-up purposes.</h4>

<p>
  <img width="1044" height="450" alt="image" src="https://github.com/user-attachments/assets/c740581f-38fa-40a6-a0c9-ca2dba82b263" />
</p>

<h4>Step 55. Creating a Ticket as an End-User on behalf of the CFO (Karen): Go to the End-User Portal URL (http://localhost/osTicket) and click "Open a New Ticket". Fill out the form as Karen Doe. Enter her Email Address, Full Name, and Phone Number. For the Help Topic, select "Report a Problem / Personal Computer Issues". In the Issue Summary, enter "CFO states he is unable to use laptop". In the Details box, enter the description: "Laptop won't power on despite pressing the power button." Once all fields are completed, click "Create Ticket" to submit the issue on behalf of the CFO.</h4>

<p>
  <img width="987" height="570" alt="image" src="https://github.com/user-attachments/assets/1366b3f5-bde8-4f02-a8b0-c786fd296234" />
  <img width="986" height="980" alt="image" src="https://github.com/user-attachments/assets/e037da4c-bf67-4560-8028-6b4184ba031e" />
  <img width="985" height="566" alt="image" src="https://github.com/user-attachments/assets/a0d3934d-baa3-408c-b3c4-2e4921ac571b" />
</p>

<h4>Step 56. Log In and Open the CFO's Ticket (John): Go to the Staff Control Panel login page (http://localhost/osTicket/scp/login.php) and log in as John. After signing in, open the Tickets tab and locate the ticket titled “CFO states he is unable to use laptop” Click the ticket number to open it and review the issue details from the help desk agent’s perspective.</h4>

<p>
  <img width="1039" height="414" alt="image" src="https://github.com/user-attachments/assets/f7d4815c-c79e-4a36-8c4b-bdaa91d1269c" />
  <img width="1031" height="619" alt="image" src="https://github.com/user-attachments/assets/7aa7c0a5-3b17-4459-a7bd-9b09fd10e9c5" />
</p>

<h4>Step 57. Update the Ticket's Priority:  In the ticket view, locate the Priority field, click “Normal”, and change the Priority Level to "Emergency". In the Reason for Update box, enter: "The CFO is unable to use his laptop, preventing him from performing critical business functions. Escalating priority to Emergency." Then click Update to apply the changes.</h4>

<p>
  <img width="1020" height="621" alt="image" src="https://github.com/user-attachments/assets/5dbf9cec-5043-412f-a633-9d83efef6a93" />
  <img width="1024" height="453" alt="image" src="https://github.com/user-attachments/assets/d90e81f5-5941-4b81-abf8-05f4280431e2" />
  <img width="1014" height="659" alt="image" src="https://github.com/user-attachments/assets/321a7f84-5128-4787-bf20-78bfac95e42f" />
</p>

<h4>Step 58. Update the CFO Ticket's SLA Plan (John): In the ticket view, locate the SLA Plan field, click on "Default SLA", and change the SLA Plan to Sev-A, since the issue affects a C-level executive who has an upcoming meeting with the board and requires the fastest possible response time. In the Reason for Update box, enter: "C-level executive impact. Assigning Sev-A for immediate attention and fastest response." Then click Update to apply the changes.</h4>

<p>
  <img width="1015" height="652" alt="image" src="https://github.com/user-attachments/assets/77314346-01e2-4c73-a0ec-6cc743a3417e" />
  <img width="1024" height="655" alt="image" src="https://github.com/user-attachments/assets/1a872d2d-e882-4ab5-8f54-a3589bd58361" />
  <img width="1010" height="657" alt="image" src="https://github.com/user-attachments/assets/e8caa780-c197-4e10-a415-cfba492b9023" />
</p>

<h4>Step 59. Update the CFO Ticket's Assigned To (John): In the ticket view, locate the Assigned To field, click "— Unassigned —" and change the Assignee to John Doe. Then click Assign to apply the changes.</h4>

<p>
  <img width="1016" height="656" alt="image" src="https://github.com/user-attachments/assets/8d12428f-0928-499a-8a58-d19ca47cb726" />
  <img width="1029" height="654" alt="image" src="https://github.com/user-attachments/assets/bd7d9ea0-4224-46d3-90af-63f1ff708b56" />
  <img width="1013" height="664" alt="image" src="https://github.com/user-attachments/assets/76dc7419-14ba-4130-9137-344de7450d10" />
</p>

<h4>Step 60. Post an Update Reply After Simulating Additional Information from the CFO (John): In the ticket view, scroll down to the Post Reply box. In the text field, enter: “CFO’s laptop was not charging due to a broken charger. Provided a new charger, and the laptop is now successfully powering on.” Then click Post Reply to add the update to the ticket.</h4>

<p>
  <img width="883" height="602" alt="image" src="https://github.com/user-attachments/assets/7459d328-a147-47a7-9d41-2840c468eede" />
  <img width="934" height="677" alt="image" src="https://github.com/user-attachments/assets/3353d956-42a7-4af4-a9a8-a19f9a73bc73" />
</p>

<h4>Step 61. Lorem</h4>

<p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h4>Part 3 Summary</h4>

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
