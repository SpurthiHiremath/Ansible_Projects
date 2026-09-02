# Ansible_Projects
This Project includes Ansible Playbooks explaining different functionalities
Web and Database Installation Using Ansible
Project Overview

This project uses Ansible to deploy a simple two-tier web application automatically.

The infrastructure contains:

A web server running Apache and PHP.
A database server running MySQL.
A common role that configures NTP on both servers.
A PHP page that connects to MySQL and displays the available databases.

The project uses Ansible roles to separate common, web-server, and database-server configuration.
he Ansible control node connects to both managed servers through SSH.

The user accesses the application through the web server.
Apache executes the generated PHP application.
PHP connects to the MySQL server.
MySQL returns the list of available databases.
Roles
Common role

The common role runs on all managed servers.

It performs the following operations:

Installs the NTP package.
Generates /etc/ntp.conf from ntp.config.j2.
Starts and enables the NTP service.
Checks the current SELinux status.
Restarts NTP when its configuration changes.
Database role

The db role runs only on hosts in the dbservers group.

It performs the following operations:

Installs MySQL and its required Python libraries.
Configures the required SELinux setting.
Generates /etc/my.cnf from my.cnf.j2.
Starts and enables the MySQL service.
Creates the application database.
Creates a database user for the web application.
Allows the database user to connect remotely.
Restarts MySQL when its configuration changes.
Web role

The web role runs only on hosts in the webservers group.

It performs the following operations:

Installs Apache, PHP, Git, and the PHP MySQL extension.
Starts and enables the Apache service.
Configures SELinux to allow Apache to connect to a remote database.
Copies or checks out the application source code.
Generates /var/www/html/index.php from index.php.j2.

Test connectivity with:

ansible all -i hosts -m ping
Running the Project

Move into the project directory:

cd Web_DB_Install_Project

Run the complete playbook:

ansible-playbook -i hosts site.yml

To request the SSH password interactively:

ansible-playbook -i hosts site.yml --ask-pass

To perform a dry-run where supported:

ansible-playbook -i hosts site.yml --check

To display additional execution details:

ansible-playbook -i hosts site.yml -v
Expected Result

After successful execution:

NTP is configured on all managed servers.
Apache and PHP are running on the web server.
MySQL is running on the database server.
The application database and database user exist.
The PHP application is available through the web server.

Open the application using:

http://<web-server-ip>/index.php
