# Ansible roles:
Ansible roles are a powerful way to structure your configuration management, allowing you to efficiently organize your files in a clear directory format. This structure not only enhances collaboration by making it easy to share roles with others, but it also promotes consistency and reusability across your projects. By adopting Ansible roles, you can streamline your processes and empower your team to work more effectively together.
The following outlines a typical role directory structure in an Ansible project:
roles/
    common/               # this hierarchy represents a "role"
        tasks/            #
            main.yml      #  <-- tasks file can include smaller files if warranted
        handlers/         #
            main.yml      #  <-- handlers file
        templates/        #  <-- files for use with the template resource
            ntp.conf.j2   #  <------- templates end in .j2
        files/            #
            bar.txt       #  <-- files for use with the copy resource
            foo.sh        #  <-- script files for use with the script resource
        vars/             #
            main.yml      #  <-- variables associated with this role
        defaults/         #
            main.yml      #  <-- default lower priority variables for this role
        meta/             #
            main.yml      #  <-- role dependencies
        library/          # roles can also include custom modules
        module_utils/     # roles can also include custom module_utils
        lookup_plugins/   # or other types of plugins, like lookup in this case

    webtier/              # same kind of structure as "common" was above, done for the webtier role
    monitoring/           # ""
    fooapp/               # ""

- **roles/**: Main directory for roles.
  
- **common/**: Reusable common role.

- **tasks/**: Contains main task definitions in a `main.yml` file, which can include smaller task files.

- **handlers/**: Defines actions triggered by tasks, with a `main.yml` file.

- **templates/**: Holds template files for the template resource, such as `ntp.conf.j2`.

- **files/**: Includes static files (e.g., `bar.txt`) and script files (e.g., `foo.sh`) for consumption by the copy and script resources.

- **vars/**: Stores role-specific variables in a `main.yml` file.

- **defaults/**: Contains default variables in a `main.yml` file with lower priority.

- **meta/**: Includes role metadata and dependencies in a `main.yml` file.



- **library/**: Houses custom modules for added functionality.

- **module_utils/**: Contains utilities for custom modules.

- **lookup_plugins/**: Holds custom lookup plugins for variable retrieval.

Additional roles, such as **webtier/**, **monitoring/**, and **fooapp/**, follow a similar organizational structure.

lab for ansible roles
=================

Create a local and remote repository named roboshop-ansible-roles and add the remote URL to the local repository. Include an inventory file in the roboshop-ansible-roles repository.
2. create roles folder in roboshop- ansible-roles folder which is very important and has everything in it
3. create mongodb folder under roles folder 
4.create tasks folder under mongodb
5. create main.yaml file under roles folder
6.under tasks create main.yaml file
To properly configure the Ansible playbook for your role, you need to create or edit the `main.yaml` file located in the `roles` directory. Follow these steps to write the necessary code:

1. Open the `main.yaml` file within the appropriate role directory.
2. Add the following code snippet to define the playbook settings:

```yaml
- name: "Install {{component}}"
  hosts: "{{component}}"
  roles:
    - "{{component}}"
```

### Explanation of the Code:
- `name`: This defines the title of the playbook task you are creating. The `{{component}}` variable will be replaced with the actual name of the component being installed, providing a clear description when the playbook runs.
- `hosts`: This specifies the target hosts where the role should be applied. Again, the `{{component}}` variable will dynamically indicate which hosts to target based on the component defined.
- `roles`: This section lists the roles that will be executed. The `{{component}}` variable indicates that the role corresponding to the specified component will be applied.

Make sure to replace `{{component}}` with the actual component name when you execute the playbook

3. Create a file named `main.yaml` within the `tasks` folder. In this file, include a comprehensive list of all the tasks that need to be performed. Make sure to detail the tasks clearly for easy understanding and implementation.
```yaml
# 4. /tasks/main.yaml
- name: Copy MongoDB repository configuration file
  ansible.builtin.copy:
    # Specifies the source file to be copied from the local machine
    src: mongo.repo
    # Destination path where the repo file will be placed on the target machine
    dest: /etc/yum.repos.d/mongo.repo
    # Set file permissions and ownership if necessary (optional)
    mode: '0644'

- name: Install MongoDB package
  ansible.builtin.package:
    # The package name for MongoDB that will be installed via the package manager
    name: mongodb-org
    # Ensures the package is present on the system
    state: present

- name: Start and enable MongoDB service
  ansible.builtin.service:
    # The name of the service that needs to be managed
    name: mongod
    # Ensures the service is started
    state: started
    # Enables the service to start on boot
    enabled: yes

- name: Allow remote connections to MongoDB
  ansible.builtin.replace:
    # The path to the configuration file that will be modified
    path: /etc/mongod.conf
    # Regular expression used to find the line that restricts connections
    regexp: '127.0.0.1'
    # The replacement text to allow connections from any IP address
    replace: '0.0.0.0'

- name: Restart MongoDB service to apply configuration changes
  ansible.builtin.service:
    # The name of the service to be restarted
    name: mongod
    # Restarts the service to ensure changes take effect
    state: restarted
``` 

This version provides clearer explanations for each task, including comments for better understanding and optional settings such as file permissions.

To execute Ansible playbooks that utilize roles, you can use the following command in your terminal:

```yaml
ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml
```

In this command:

- `ansible-playbook` is the Ansible command used to run playbook files.
- `-i inventory.ini` specifies the inventory file that lists the servers on which the playbook will be executed.
- The `-e` flag allows you to pass extra variables to the playbook. In this case:
  - `ansible_user=centos` sets the username for SSH access to the servers.
  - `ansible_password=DevOps321` provides the password for that user account.
  - `component=mongodb` defines a variable named `component` with the value `mongodb`, which can be referenced within the playbook.
- `main.yaml` is the name of the playbook you are executing, which is located in the roles folder. This playbook will contain tasks that are designed to configure or manage the specified component, in this case, MongoDB. 

Make sure to have the necessary permissions and that the Ansible environment is correctly set up to avoid any execution issues.
