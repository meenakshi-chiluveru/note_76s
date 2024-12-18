ansible features
1. platform independent
2. scalable
3. idempotence
4. error handling
5. vault
6. rich modules
7. agent less
 # ansible following push based architechture
 lab: create 2 servers name them as ansible and node
 write multiplaybook in IDE
 - name: PLAY-1
  hosts: localhost
  tasks:
  - name: PLAY-1 and task1
3. login servers through putty
4. clone the repo and run the playbook - ansible-playbook -i inventory.ini -e ansible_user=centos -e
 ansible_password=DevOps321 03-multyplay.yaml

vriables in ansible

variables can be given by vars
task level variables can be override play level variables


 
 
**Ansible Features**

1. **Platform Independence:** Ansible can operate across various platforms without restrictions, making it versatile.
2. **Scalability:** It is designed to efficiently manage numerous servers, growing with your infrastructure needs.
3. **Idempotence:** Ansible ensures that running the same playbook multiple times does not change the system's state when it is already configured correctly.
4. **Error Handling:** It includes robust mechanisms for managing errors, enhancing reliability during automation tasks.
5. **Vault:** Ansible Vault allows you to secure sensitive information, such as passwords and API keys.
6. **Rich Modules:** It offers a wide range of modules that facilitate various automation tasks, providing flexibility and functionality.
7. **Agentless:** Ansible operates without requiring agent installation on target machines, simplifying setup and maintenance.

**Architecture**

Ansible utilizes a push-based architecture, which simplifies the process of managing remote systems.

**Lab Setup**

1. **Server Creation:** Create two servers and label them "ansible" and "node."
2. **Multi-Playbook Development:** Write a multi-playbook using your preferred IDE.

**Example Multi-Playbook**

```yaml
- name: PLAY-1
  hosts: localhost
  tasks:
    - name: PLAY-1 Task 1
```

3. **Server Login:** Access the servers using PuTTY for command execution.
4. **Executing the Playbook:** Clone the repository and run the playbook with the following command:

```bash
ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 03-multi-play.yaml
```

**Variables in Ansible**

In Ansible, you can define variables using the `vars` keyword. Additionally, task-level variables can be set to override those defined at the play level, offering flexibility in configuration management. 

By leveraging Ansible's features and following these steps, you can effectively streamline your automation processes and enhance your infrastructure management.
