**Ansible_Web_Deployment**

This Ansible project deploys a web application to multiple servers using reusable roles. 
The common role installs basic packages, while the webserver role installs Apache, backs up the existing application, 
deploys a new page, starts the service, and verifies the application using an HTTP health check. 
The serial: 2 setting updates only two servers at a time. The health check uses register to save its result, retries
and delay to repeat the check, and until to continue until the application responds successfully.
If any task inside the block fails, the rescue section attempts to restore the previous application and reports the failure. 
The always section runs regardless of success or failure and records that the deployment attempt has finished.
**
Execution**

ansible-playbook site.yml --syntax-check

ansible-playbook site.yml
