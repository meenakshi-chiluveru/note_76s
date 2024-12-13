To establish a connection to a node via an Ansible server, you can use the following command: 

```bash
ansible -i public_ip, all -e ansible_user=centos -e ansible_password=DevOps321 -m ping
```

In this command, we are specifying the inventory using `public_ip`, targeting all hosts. The `-e` flag is used to define extra variables, which in this case include the username (`centos`) and password (`DevOps321`) for authentication. The `-m ping` part of the command indicates that we are invoking the 'ping' module, which is a simple test to check the connectivity to the specified nodes. 

In Ansible, commands are executed using modules, which are reusable scripts that perform specific tasks on the managed nodes.

To effectively install a package using Ansible modules, you can utilize the following command:

```bash
ansible -i public_ip, all -e ansible_user=centos -e ansible_password=DevOps321 --become -m yum -a "name=nginx state=present"
```
there is no sudo command in ansible we have give --become to becoming root user
This command allows you to connect to a specified remote server and install the Nginx web server. Let’s break down the key components for a clearer understanding:

- **ansible**: This is the primary command-line tool used for managing and interacting with remote machines via Ansible.
- **-i public_ip,**: Here, you specify the inventory of hosts, with `public_ip` being the address of the target server. The trailing comma indicates that you are working with a single entry.
- **all**: This signifies the target host group; using `all` means that the command will be executed on every host listed in the inventory.
- **-e ansible_user=centos**: This option allows you to define the username for the connection, which in this scenario is `centos`.
- **-e ansible_password=DevOps321**: This option specifies the password required for the user account on the remote server, ensuring smooth authentication.
- **-m yum**: By using the `yum` module, you are leveraging the appropriate tool for managing packages in CentOS and similar distributions.
- **"name=nginx state=present"**: This command portion indicates that you want to install the `nginx` package, ensuring that its state is set to 'present'—meaning it will be installed if it's not already available on the system.

By using this command, you can streamline the installation process of the Nginx web server on your remote server, enhancing your overall deployment efficiency with Ansible.

ansible -i public_ip, all -e ansible_user=centos -e ansible_password=DevOps321 --become -m service -a "name=nginx state=started" - to start the service

playbook: a file of modules/collections
playbook has YAML syntax [yet another markup language]

This document presents an Ansible playbook structured to manage user information. Below are the details for two individuals:

the below is ansible playbook
- name: sivakuamr
  dob: "2023-09-09"
  address:
    address-line1: vivek strret
    address-line2: sanath nagar
    city: HYD
  email: info@joindevops.com
- name: ramesh
  dob: "33333"
  address:
  - address-line1: vivek
    address-line2: sanath
    city: hyd1
  - address-line1: vivek strret2
    address-line2: sanath nagar
    city: HYD2
  email: info@joindevops.com
    
  - 
   
