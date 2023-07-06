# Ansible Playbook for PHP-Based Website Environment Setup
📜 With the help of this Ansible playbook, you can quickly set up a PHP-based website environment with Nginx Web-server on a fresh Linux machine. This playbook automates the deployment process and installation processes, making use of Ansible's strength 💪 and adaptability. It ensures consistency and minimizes manual setup efforts.

⚙️ By leveraging the power of Ansible, you can easily replicate and scale your PHP-based website environment across multiple servers with minimal effort. Enjoy the simplicity ✨ and efficiency ⚡ provided by this playbook, ensuring a consistent and reliable setup for your web applications. 🚀

⚠️ Please ensure that you have SSH access to the target server(s) with the appropriate credentials for Ansible to connect and execute commands remotely 🖥️.

# Install Ansible on Linux

To install Ansible on Linux, follow these steps:

1) Add the Ansible repository to your system's package manager:

```
$ sudo apt-add-repository ppa:ansible/ansible
```

2) Update the package lists to include the newly added repository:

```
$ sudo apt update
```

3) Install Ansible:

```
$ sudo apt install ansible
```

4) Verify the Ansible installation by checking the version:

```
$ ansible --version
```
The output should display the installed Ansible version information, confirming that the installation was successful.

# Pre-installation for run code

- For the create MySQL related user on the target server need to install it in the machine where you are performing this Ansible file.

```
$ ansible-galaxy collection install community.mysql
```

# Setup Ansible-Hosts file

The /etc/ansible/hosts file is the inventory file used by Ansible to define and organize the hosts (remote servers) that Ansible will manage. It is a text file that lists the hostnames or IP addresses of the remote servers and organizes them into groups.

Where,

[test] = Your target server name.

Replace 3.111.217.83 with your target server IP(s).

```
$ sudo nano /etc/ansible/hosts
```


```
# Ansible-Target-Server
[test]
3.111.217.83 ansible_ssh_private_key_file=/home/$USER/.ssh/id_rsa
```

# Ansible Playbooks for Server Configuration

This repository contains a collection of Ansible playbooks and configuration files to automate the setup and configuration of a server. Below is a brief description of each file and its purpose.

##  Installing code

1) Clone code on your machine.

```
$ git clone https://github.com/vcian/ansible-php-nginx-setup.git
```

2) Enter in Direcotry.

```
$ cd php-ansible-setup
```

3) Run Playbook.

```
$ ansible-playbook *.yml
```


## Project-structure

```
.
├── 01_check_connection.yml
├── 02_install_mysql.yml
├── 03_database_user.yml
├── 04_install_php.yml
├── 05_install_nginx.yml
├── 06_download_adminer.yml
├── 07_nginx-default_overwrite.yml
├── 08_restart_FPM-Nginx.yml
├── conf
│   └── default
└── README.md

1 directory, 10 files
```

### Ansible-playbook Details

This repository contains a collection of Ansible playbooks that can be used to automate various tasks related to server setup and configuration. Each playbook is designed to perform a specific task and can be executed individually or as part of a larger workflow.

`01_check_connection.yml`
- This playbook checks the SSH connectivity to the target server to ensure that Ansible can establish a connection.

`02_install_mysql.yml`
- This playbook installs the MySQL database server on the target server.

`03_database_user.yml`
- This playbook creates a new user and database in MySQL. It prompts for the desired username, password, and database name during execution.

`04_install_php.yml`
- This playbook installs PHP 8.1 on the target server.

`05_install_nginx.yml`
- This playbook installs the Nginx web server on the target server.

`06_download_adminer.yml`
- This playbook downloads and sets up the Adminer database management tool.

`07_nginx-default_overwrite.yml`
- This playbook overwrites the default Nginx configuration file with a custom configuration specific to adminer access with IP/*.php needs.

`08_restart_FPM-Nginx.yml`
- This playbook restarts the PHP-FPM and Nginx services to apply the configuration changes and update the upgrade the value of 
`upload_max_filesize` & `post_max_size` & `memory_limit` after restart php fpm. 

`conf/default`
- The default file is a sample Nginx configuration file that can be used as a starting point for your specific server configuration. You can modify it as needed to serve your application.

Please note that before executing these playbooks, you should update the necessary variables (vars) and configurations according to your environment and requirements.

## **Warning**

Assuming you've gone so far as to get Ansible running and have downloaded these playbooks, you probably understand how this stuff works and how much damage it could do. But just in case, These playbooks will remove data, destroy accounts and wreak havoc if pointed to the wrong account. Please be careful, keep backups and read the code before running it.