# Red Hat Image Builder Automation & Red Hat Image Builder Automation for Azure Deployment
----------------------------
This is a starter kit for automation of Red Hat image builder and deploying to azure with ansible. This repository is intended for users to get familiar with automating Red Hat image builder, and to get started pushing images to the cloud like Azure , G.C.P and etc. I welcome others to come and work on this project because at the time of this publishing (08/10/2021) there isn't any documentation on ansible and red hat image builder running together. 

Prerequisites
------------------

--------------------------------
2x Red Hat Enterprise Linux Server 8.4  \
1x Ansible or Ansible Automation Platform \
1x Red Hat Image Builder \
1x Microsoft Azure Account

------------------------------
How to use 
--------------
1. Install Red Hat Enterprise Linux for two systems. One Red Hat Enterprise Linux system will be designated for Ansible Automation Platform or Ansible (user-preference), and you will need a second Red Hat Enterprise Linux system for Red Hat Image builder . Once the installation for ansible is complete , please be sure to configure the inventory file so you're able to connect to your host(s) (if you're using ansible-cli), and if you're using Ansible Automation platform be sure to configure "credentials" (for authentication),"projects"(for source code/files) "inventory" (for hosts in your environment). If you use Ansible Automation Platform, you will have to construct job templates to utilize the roles and playbooks provided in this repository. 
2. On the Red Hat Enterprise Linux System that is designated for Red Hat Image Builder, please install the correct packages for composer-cli/os-build/lorax consult this article for assistance https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/composing_a_customized_rhel_system_image/installing-composer_composing-a-customized-rhel-system-image . The environment should work with os-build, however, if running to issues executing os-build, use lorax. Be sure to consult the previous article if you run into issues with user and group permissions with lorax or os-build. If you run and execute the ansible or the red hat enterprise linux image builder system in root, there shouldn't be any issues with image builder. However, it is possible that running under different users you will need to add group permission. 
3. It is also important to note that you will need to install azure-cli on the system designated for Red Hat Image Builder. Consult this article https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=dnf for more information on how to do that(tobecontinued). Whenever you log into azure through the cli, you'll notice the playbook uses the parameters of -u and -p. This is because for us to logn into our account we must define those parameters, if we do not define those parameters in our playbook, the playbook will fail because "az login" will prompt us with a web-browser instead of prompting us through the cli. Also, executing "az login" in root with any parameters will fail because it isn't supported. 
4. When you begin to intitilia
