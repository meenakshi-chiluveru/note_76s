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
