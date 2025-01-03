### Understanding File Permissions in Linux

In Linux, file permissions are crucial for managing access to files and directories. Each file or directory has three types of permissions: read (r), write (w), and execute (x). These permissions can be assigned to three categories of users: 

- **User (u)**: The owner of the file.
- **Group (g)**: Other users who are members of the file's group.
- **Others (o)**: All other users.

#### Permission Values
Each permission type is represented by a numerical value:
- Read (r) = 4
- Write (w) = 2
- Execute (x) = 1

When combined, these values determine the overall permission level. For instance, a permission string might look like this: `-rw-rw-r--`.

### Example of Permission Structure
The example below illustrates a file's permission:
```
-rw-rw-r-- 1 ec2-user (user) ec2-user (group) 0 Nov 22 13:27 sample
```
In this case, the file named `sample` is owned by the user `ec2-user`, and it belongs to the group `ec2-user`. The permissions indicate that the user and group have read and write access, while others have only read access.

### Managing Permissions Using chmod
The `chmod` command is used to change file permissions. Here are some examples:

1. To add execute permission for the user:
   ```
   chmod u+x sample
   ```

2. To remove read and write permissions for the group:
   ```
   chmod g-rw sample
   ```
   The resulting permissions would change to `-rwx---r--`.

3. To remove read permissions for others:
   ```
   chmod o-r sample
   ```
   The permissions would then appear as `-rwx------`.

4. To grant read permissions to everyone:
   ```
   chmod ugo+r sample
   ```
   This changes the permissions to `-rwxr--r--`.

5. To grant execute permissions to group and others:
   ```
   chmod go+x sample
   ```
   The final permissions could be displayed as `-rwxr-xr-x`.

### Recursive Permission Changes
When changing permissions for directories, you can apply changes to all files within those directories using the `-R` flag. For example, removing write permissions for the group recursively from a directory named `devops` can be done with:
```
chmod g-w -R devops/
```
This will apply the permission change to all files and subdirectories within `devops`.

### Specific Permission Settings
You can also set specific permissions using numeric values. For instance:
- Setting read, write, and execute permissions for the user (7), read permissions for the group (4), and no permissions for others (0) looks like this:
  ```
  chmod 740 example.txt
  ```
  After running this command, the permissions would show as `-rwxr-----`.

- Similarly, to set read, write, and execute permissions for the user (7), read and execute for the group (5), and no permissions for others (1), the following command can be used:
  ```
  chmod 751 example.txt
  ```
  This sets the permissions to `-rwxr-x--x`.

By understanding and using file permissions effectively, you can maintain better control over access and security on your Linux systems.

### User Management in DevOps

In our DevOps teams, we recently welcomed Ramesh as a new member. Here's a detailed overview of the user management process for creating and configuring a new user in our system.

#### Steps to Create a New User

1. **Create User Command**: To add a new user named Ramesh to the system, we use the following command:
   ```bash
   sudo useradd ramesh
   ```
   This command creates a new user account with the username 'ramesh'.

2. **Set User Password**: After creating the user, it's important to set a password. This can be done with the command:
   ```bash
   passwd ramesh
   ```
   This prompts you to enter and confirm a new password for Ramesh's account.

3. **User and Group Association**: When a new user is created, a corresponding group with the same name is automatically generated. You can view all user entries in the system by checking the `/etc/passwd` file.

4. **List Current Groups**: To see all the groups available, you can run:
   ```bash
   getent groups
   ```

#### Configuring SSH Access for the New User

To enable SSH access for Ramesh, some configuration steps are necessary:

1. **Edit the SSH Configuration**: Open the SSH daemon configuration file using the `vim` editor:
   ```bash
   vim /etc/ssh/sshd_config
   ```
   In this file, locate the line that specifies password authentication and change it to:
   ```
   PasswordAuthentication yes
   ```
   This allows users to authenticate via password.

2. **Check Configuration Syntax**: Before restarting the SSH service, it’s good practice to check the syntax of the configuration file to avoid any errors:
   ```bash
   sshd -t
   ```

3. **Restart the SSH Service**: After confirming that there are no syntax errors, restart the SSH service to apply the changes:
   ```bash
   systemctl restart sshd
   ```

#### Connecting to the Server

Once the configuration is complete, Ramesh can connect to the server using SSH. The command for this would look like:
```bash
ssh ramesh@18.215.175.191
```
Upon executing this command, the terminal prompts Ramesh to enter his password.

#### Example SSH Session

Upon successful authentication, he might see something like this at the beginning of his SSH session:

```
Welcome to Amazon Linux 2
End of Life is 2025-06-30.
A newer version of Amazon Linux is available!
```

#### Verifying User Directory

After logging in, Ramesh can confirm his current working directory with the command:
```bash
pwd
```
This should display his home directory, typically shown as:
```
/home/ramesh
```

This comprehensive guide outlines the steps involved in user management and SSH configuration in a DevOps environment, ensuring that new users can be set up securely and efficiently.

To create a new user group named "devops," you would use the command:

```bash
groupadd devops
```

It's important to note that each user on the system is assigned a primary group and can be associated with one or more secondary groups. For example, if we want to add a user named "ramesh" to the "devops" group, we can accomplish this with the following command:

```bash
usermod -g devops ramesh
```

After executing this command, you can verify ramesh's group assignments using the command:

```bash
id ramesh
```

Now, regarding file ownership, the `chown` command is used to change the owner of a file. However, it's essential to understand that even the owner of a file is unable to modify its ownership unless they have the proper permissions. Only a user with sudo privileges can perform ownership changes. To change the ownership of a file named "example" to ramesh and set the group to "devops," you would use the following command:

```bash
chown ramesh:devops example
```

This command will ensure that ramesh becomes the owner of the file, and the file will be associated with the devops group.

To delete a user from a specific group, you can use the following command: `gpasswd -d username groupname`. It’s important to ensure that the user is removed from any associated groups before proceeding with their deletion from the organization.

First, if you need to manage project releases or company releases, make sure that the necessary user adjustments are made prior to these activities.

To completely remove a user, you can use the command: `userdel username`. 

If you also need to delete a group (for instance, a group named "ramesh"), you can accomplish this with the command: `groupdel ramesh`. 

Always ensure to follow proper procedures when modifying user and group settings within your organization.

to change ownership to folder
To change the ownership of a folder and all of its contents recursively, use the command: `chown user:group -R folder`. This command assigns the specified user and group as the new owners of the folder and every file and subfolder it contains.

To enable SSH access for a new user through a public key, follow these detailed steps:

1. **Generate SSH Keys**: Start by generating a pair of SSH keys (a public key and a private key). It's important to keep the private key secure. Request the public key from the person who will be logging in.

2. **Set Up the SSH Directory**: Navigate to the newly created user's home directory:
   ```bash
   cd /home/raheem
   ```
   Create a directory named `.ssh`, which will store the user's SSH keys:
   ```bash
   mkdir .ssh
   ```

3. **Set Permissions**: Ensure that the `.ssh` directory has the correct permissions by running the following command:
   ```bash
   chmod -R 700 .ssh
   ```

4. **Generate the Key Pair**: Use the SSH key generation command to create the key pair. Make sure to use the correct command, `ssh-keygen`:
   ```bash
   ssh-keygen -f raheem
   ```

5. **List Files**: After generating the keys, list the contents of the current directory to confirm:
   ```bash
   ls -la
   ```

6. **Navigate to the .ssh Directory**: Move into the newly created `.ssh` directory:
   ```bash
   cd .ssh/
   ```

7. **Edit the Authorized Keys File**: Open the `authorized_keys` file in a text editor, such as `vim`, to store the public key:
   ```bash
   vim authorized_keys
   ```

8. **Paste the Public Key**: Paste the public key provided by the user into the `authorized_keys` file. This will enable SSH access using the corresponding private key.

9. **Set Permissions on Authorized Keys**: Secure the `authorized_keys` file by setting the appropriate permissions:
   ```bash
   chmod 400 authorized_keys
   ```

10. **Adjust Ownership**: Ensure that the `.ssh` directory and its contents are owned by the user "raheem":
    ```bash
    chown -R raheem:raheem .ssh
    ```

11. **SSH into the User Account**: Finally, to connect to the server as "raheem," use the following command, replacing `ipaddress` with the actual IP address of the server:
    ```bash
    ssh -i raheem raheem@ipaddress
    ```

By following these steps, you can successfully set up SSH access for the user "raheem" using a private key.

process management
--------------------------------------------
everything in linux is process
teamleader
team manager
account manager
senior eng
junior eng
traine

team leader - 1 ticket created about devops pipeline setup =1
senior engineer =1
subtask -2 -junjor engineer
subtask =3 - -junjor engineer-2
=========================
In Linux, whenever we initiate any action or command, the system generates a unique Process ID (PID) that is reported back to us. For example, if we run the command `ps`, we can view the list of currently active processes along with their respective PIDs. Here’s a sample output:

```
PID TTY TIME CMD
3720 pts/0 00:00:00 sudo
3721 pts/0 00:00:00 bash
3738 pts/0 00:00:00 ps
```

In this output, you can see that the PID for the `sudo` command is 3720, while the `bash` shell has a PID of 3721, and the `ps` command itself is assigned a PID of 3738.

When we use the command `echo hello`, we are instructing the system to print the text "hello" to the terminal. This task is also assigned a PID for tracking.

To create a new process ID, an example PID could be 2345, which would be associated with the `bash` shell that initiated the command.

If we want to see a comprehensive list of all running processes in Linux, we can use the command `ps -ef`. This provides detailed information about each active process, which can help us monitor system activity effectively.

In Linux, processes can be categorized into two main types: 

1. **Foreground Process**: This type of process runs in the foreground and is directly associated with the terminal session. It takes input from the user and displays output directly in the terminal. Users can interact with it, pausing or stopping it as needed.

2. **Background Process**: In contrast, a background process runs independently of the terminal session. It operates behind the scenes, allowing the user to continue using the terminal for other tasks. Background processes are often initiated with a specific command to run in the background.

To check whether a specific process, such as "jenkins," is currently running, you can use the command `ps -ef | grep jenkins`. This command lists all running processes, and the `grep` command filters the results to show only those related to "jenkins."
 
When a process becomes unresponsive and gets stuck, it's necessary to terminate it to free up system resources. You can use the command:

```
kill [process ID]
```

This command allows you to target a specific process instance by its unique ID. It's important to ensure that you only terminate the intended process and avoid interfering with its parent process.

If the process remains unresponsive and does not terminate with the regular kill command, you can forcefully terminate it using the following command:

```
kill -9 [process ID]
```

The `-9` option sends a SIGKILL signal, which forcefully stops the process immediately, bypassing any cleanup operations. Use this command cautiously, as it may lead to data loss or corruption.


### Package Management Overview

When managing software packages on systems like Red Hat Enterprise Linux (RHEL), CentOS, Fedora, or Amazon Linux 2, the `yum` package manager is a critical tool. Here’s a brief guide on how to use `yum` effectively:

- **Installing Packages:** To install a specific package, use the command:
  ```
  yum install <packagename>
  ```
  Replace `<packagename>` with the name of the software you wish to install.

- **Checking Installed Packages:** If you need to see which packages are currently installed on your system, you can run:
  ```
  yum list installed
  ```
  To filter this list and find a specific package, such as Git, use:
  ```
  yum list installed | grep git
  ```

- **Listing Available Packages:** To view all packages that are available for installation, use:
  ```
  yum list available
  ```

- **Counting Available Packages:** If you want to know how many packages are available, you can count them with:
  ```
  yum list available | wc -l
  ```

- **Searching for Specific Software:** If you’re looking for a particular package, like MySQL, you can search for it using:
  ```
  yum search MySQL
  ```

- **Removing Packages:** To uninstall a package, such as Git, you can execute:
  ```
  yum remove git -y
  ```
  The `-y` flag automatically confirms the removal without prompting.

- **Installing Web Server:** To quickly set up an Nginx web server, you can run the command:
  ```
  yum install nginx -y
  ```

By utilizing these commands, you can effectively manage software on your Linux system.
