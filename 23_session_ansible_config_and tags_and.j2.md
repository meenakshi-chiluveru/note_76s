The `ansible.cfg` file is the configuration file for Ansible, which defines various settings and parameters for your Ansible environment. The configuration can be established in several locations, with the following hierarchy:

1. **ANSIBLE_CONFIG**: This is an environment variable that, if set, specifies the path to the Ansible configuration file. It takes precedence over other configuration files.

2. **ansible.cfg in the current directory**: If no environment variable is set, Ansible will look for the `ansible.cfg` file in the current working directory where the Ansible command is executed.

3. **~/.ansible.cfg**: If a configuration file is not found in the current directory, Ansible will then check for the `ansible.cfg` file in the user's home directory (referred to as the "tilde" or `~`).

4. **/etc/ansible/ansible.cfg**: Finally, if none of the above configuration files are found, Ansible will default to the system-wide configuration file located at `/etc/ansible/ansible.cfg`.

This order of precedence means that the configuration file found in the current directory will override the one in the home directory, and the home directory configuration will override the system-wide configuration.

# lab
To set up your Ansible configuration, first, create a file named `ansible.cfg` in the current directory. Within this file, include the following lines under the `[defaults]` section:

```
[defaults]
inventory=inventory.ini
ansible_user=centos
```

Next, create an `inventory.ini` file, where you will specify the variables for all hosts. Within this file, add the following lines to define the Ansible password:

```
[all:vars]
ansible_password=DevOps321
```

This setup allows you to define the inventory and user details required for your Ansible automation tasks.

To initiate the setup for the catalogue role, begin by creating a new folder called "template" inside the existing catalogue role directory. This structure will help in organizing your files effectively. Once the template folder is created, proceed to copy the catalogue service file from its original location into this new template folder.

After copying the service file, it is essential to change its file extension to .j2. This extension signifies that the file uses Jinja2 templating format, which allows for dynamic content replacement when the template is processed. It should be noted that in a Linux environment, the file extension does not affect the ability to execute the file, but using .j2 assists in clearly identifying its purpose.

As part of the template configuration, you will need to replace any hardcoded references to "mongod.daws80.online" within the service file with the variable placeholder "{{MONGODB_HOST}}." This step makes the configuration more flexible and allows for the use of different host values without altering the template itself.

In parallel, you should create a new file named "variables.yaml" within the "roboshop-ansible-roles" directory. This file is crucial for defining the variables that will be used throughout your playbooks. In "variables.yaml," include the following line to set the MongoDB host variable:

```yaml
MONGODB_HOST: mongodb.daws80.online
```

This line establishes a key-value pair indicating that the variable `MONGODB_HOST` will hold the value `mongodb.daws80.online`.

Next, when you define your main YAML playbook, you will integrate this variable. Structure your playbook as follows:

```yaml
- name: "install {{component}}"
  hosts: "{{component}}"
  vars:
    - variables.yaml
  become: yes
  roles:
    - "{{component}}"
```

In this snippet, the playbook specifies a task titled "install {{component}}," where `{{component}}` is a placeholder for the actual component name that will be defined during execution. The `hosts` directive is set to `{{component}}` as well, allowing the playbook to target the appropriate servers. The `vars` section includes a reference to "variables.yaml," ensuring that the variables defined there are accessible. The `become: yes` directive indicates that the tasks will be executed with elevated privileges, which is often necessary for installation tasks. Finally, the `roles` section specifies the role corresponding to the component being installed, further utilizing the dynamic component placeholder.

This detailed configuration not only organizes your files but also enhances flexibility and maintainability in your Ansible setup for the catalogue role.
=======================================================
- name: "Copy {{component}}.service"
  ansible.builtin.template
    src: "{{component}}.service.j2"
    dest: "/etc/systemd/system/{{component}}.service"

3.In the project, there is a requirement to copy a systemd service file using Ansible. The specific Ansible module used for this task is the `ansible.builtin.template` module. The source template file is named `{{component}}.service.j2`, and it will be copied to the destination path `/etc/systemd/system/{{component}}.service`. Additionally, it has been instructed to place this module within a common folder that contains a configuration file called `systemd.yaml`, while also including a comment indicating the purpose of the copy module.
