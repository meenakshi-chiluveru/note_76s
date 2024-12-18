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


 
 
