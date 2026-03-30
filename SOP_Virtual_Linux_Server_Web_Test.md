![_3d03e585-ebf5-4a6f-a556-50aee3ea16e5](https://github.com/user-attachments/assets/4b01f5c5-3b61-4c31-af2d-fe3ca0e0469e)

SOP – Setting Up a Virtual Linux Server for Web Application Testing
1. Title
Standard Operating Procedure: Creating a Virtual Linux Server for Web Application Testing
________________________________________
2. Purpose
The purpose of this SOP is to walk through the process of setting up a virtual Linux server that can be used for testing web applications. The idea is to make sure the setup is consistent every time, so anyone following these steps ends up with the same working environment. This helps avoid configuration mistakes and keeps our testing process predictable.
________________________________________
3. Scope & Objectives
Scope
This document covers everything from creating the virtual machine to installing the web stack and confirming that the server is ready for testing.
Objectives
•	Build a VM with medium level resources suitable for general web testing
•	Install Ubuntu Server 22.04 LTS
•	Set the hostname to hamayoun.arshad
•	Use NAT networking so the VM can access the internet
•	Install a LAMP stack (Apache, MariaDB, PHP)
•	Make sure the server is reachable and able to run test applications
________________________________________
4. Accountability Matrix
Task	Role	Responsibility
VM setup	System Administrator	Create the VM and assign resources
OS installation	System Administrator	Install Ubuntu and basic system settings
Network setup	System Administrator	Make sure NAT networking works
Web stack installation	QA Engineer	Install Apache, MariaDB, PHP, and tools
Server testing	QA Engineer	Confirm the server works for web testing
Documentation	Technical Writer	Update and maintain this SOP

________________________________________
5. Revision History
Version	Date	Author	Description
1.0	Mar 30, 2026	Hamayoun Arshad	First version created
1.1	Apr 2, 2026	QA Team	Small edits and cleanup
________________________________________
6. Prerequisites
Before starting, make sure you have:
•	VirtualBox or VMware Workstation installed
•	Ubuntu Server 22.04 LTS ISO file
•	A computer with at least 8 GB RAM, 4 CPU cores, and 50 GB free storage
•	Internet access
________________________________________
7. Procedure
7.1 Create the Virtual Machine
1.	Open your hypervisor and click Create New Virtual Machine.
2.	Use the following settings: 
o	CPU: 2 vCPUs
o	RAM: 4 GB
o	Disk: 40 GB (dynamic is fine)
o	Network: NAT
3.	Attach the Ubuntu Server ISO.
4.	Start the VM.
________________________________________
7.2 Install Ubuntu Server
1.	Choose Install Ubuntu Server from the boot menu.
2.	Pick your language and keyboard layout.
3.	When asked for a hostname, enter:
hamayoun.arshad
4.	Create a local admin user.
5.	Use the default guided partitioning.
6.	Let the installation finish and reboot.
________________________________________
7.3 Check Networking
1.	Make sure the VM has an IP address: 
2.	ip a
3.	Test internet access: 
4.	ping -c 3 google.com
5.	Update the system: 
6.	sudo apt update && sudo apt upgrade -y
________________________________________
7.4 Install the Web Stack (LAMP)
Install Apache
sudo apt install apache2 -y
Install MariaDB
sudo apt install mariadb-server -y
sudo mysql_secure_installation
Install PHP and modules
sudo apt install php php-mysql php-cli php-xml php-curl php-zip -y
Install helpful tools
sudo apt install git curl unzip ufw -y
________________________________________
7.5 Set Up the Firewall
1.	Allow web traffic: 
2.	sudo ufw allow 80/tcp
3.	Turn on the firewall: 
4.	sudo ufw enable
________________________________________
7.6 Test the Web Server
1.	Check Apache: 
2.	systemctl status apache2
3.	On your host machine, open a browser and go to:
http://<VM-IP>
4.	You should see the default Apache page.
________________________________________
7.7 Optional: Add a Simple Test App
1.	Download a sample PHP app: 
2.	cd /var/www/html
3.	sudo git clone https://github.com/example/sample-php-app testapp
4.	Restart Apache: 
5.	sudo systemctl restart apache2
6.	Open the test app in your browser.
________________________________________
7.8 Save Notes and Create a Snapshot
1.	Write down the VM specs and installed packages.
2.	Save your notes in your GitHub repo.
3.	Create a VM snapshot so you can return to this setup later.
________________________________________
8. Approval Table
Name	Role	Action	Date
Hamayoun Arshad	Author	Wrote SOP	Mar 30, 2026
QA Lead	Reviewer	Reviewed SOP	Apr 1, 2026
IT Manager	Approver	Approved SOP	Apr 2, 2026
