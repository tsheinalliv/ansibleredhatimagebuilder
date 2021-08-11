# Red Hat Image Builder Automation & Red Hat Image Builder Automation for Azure Deployment
----------------------------
This is a starter kit for automation of Red Hat image builder and deploying to azure with ansible. This repository is intended for users to get familiar with automating Red Hat image builder, and to get started pushing images to the cloud like Azure , G.C.P and etc. I welcome others to come and work on this project because at the time of this publishing (08/10/2021) there isn't any documentation on ansible and red hat image builder running together. This project also assumes that the users viewing already have experience with ansible and red hat image builder. 

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
------------
2. On the Red Hat Enterprise Linux System that is designated for Red Hat Image Builder, please install the correct packages for composer-cli/os-build/lorax consult this article for assistance https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/composing_a_customized_rhel_system_image/installing-composer_composing-a-customized-rhel-system-image . The environment should work with os-build, however, if running to issues executing os-build, use lorax. Be sure to consult the previous article if you run into issues with user and group permissions with lorax or os-build. If you run and execute the ansible or the red hat enterprise linux image builder system in root, there shouldn't be any issues with image builder. However, it is possible that running under different users you will need to add group permission. 
----------------------
3. It is also important to note that you will need to install azure-cli on the system designated for Red Hat Image Builder. Consult this article https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=dnf for more information on how to do that. Whenever you log into azure through the cli, you'll notice the playbook uses the parameters of -u and -p. This is because for us to logn into our account we must define those parameters, if we do not define those parameters in our playbook, the playbook will fail because "az login" will prompt us with a web-browser instead of prompting us through the cli. Also, executing "az login" in root with any parameters will fail because it isn't supported. 
---------------------------
4. Once you have both environments configured (by the way I encorage any users/friends of this project to automate some of these processes such as setting up image builder and deploying azure-cli to re-enforce automation across this project), you can begin to configure the .toml file in the repository to configure the image you want to deploy. Consult this article on how to configure the.toml file https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/composing_a_customized_rhel_system_image/creating-system-images-with-composer-command-line-interface_composing-a-customized-rhel-system-image#composer-command-line-interface_creating-system-images-with-composer-command-line-interface .There are two ways to utilize this project either through using "roles" (which is under azurecloud_imagebuilder-deployment_kit) or "playbooks." I'd suggest using roles if you plan to build on this project or your own project and deploy in different environments. If you are looking for an automation process to deploy static then I'd reccomend just consuming .toml file and the following playbooks. 
-----------------------------
5. Once you have the .toml file configured , the first playbook you will utilize is "compose_imagebuild.yml." Be sure to configure the correct hosts in your environmenet, and configure the "hosts:" selector option with the designted Red Hat Enterprise Linux Image Builder system. From there, if you're using ansible, it is a simple "ansible-playbook compose_imagebuild.yml ( be sure to configure "sudo" and privelege escalation or you may run into problems). If you're using ansible automation platform, it is simply initializing a job template. Once the playbook has been completed , there will be information of the status of your image build. In able for you to utilize the next playbook, you must gather the UUID of the image you just created. That UUID sting will be the first string  that has been displayed as a result of "composer-cli compose status"  on your ansible terminal, it will be a string of characters and numbers. That will be copied and pasted into two of the variables on the next playbook (again, I encourage any users to automate this process by dumping the uuid into a text file or pulling that string to be automated instead of manually placed into a playbook. (tobecontinued---this is still under construction)
