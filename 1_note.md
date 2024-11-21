Linux uses an SSH authentication mechanism that involves a pair of keys: a public key and a private key. The Linux server is often referred to as the "server" or "box."

The public key will be stored on the Linux box, while the private key will be kept secure with you.

To generate a key pair, use the following command:

```bash
ssh-keygen -f <file-name>
```

This command can be executed in Git Bash, which is essentially a mini Linux environment in Windows. By default, Git Bash will log in to the path `/c/users/username`.

To generate a key pair named "daws-76s," you would enter the command:

```bash
ssh-keygen -f daws-76s
```

If prompted for a passphrase, you can simply press enter to skip this step.

After executing the command, two files will be generated:

- `daws-76s.pub` (the public key)
- `daws-76s` (the private key)
````````````````````
# Enabling File Extensions for Known File Types
To enable file extensions for known file types, follow these steps:
1. Open the Control Panel.
2. Navigate to File Explorer Options.
3. Go to the "View" tab and uncheck the option "Hide extensions for known file types."

## Public Key Syntax
The syntax for a public key is as follows:
```
ssh-rsa <code> <laptop-name>
```

## Overview of Amazon EC2

Amazon EC2 (Elastic Compute Cloud) is a service provided by AWS that enables you to create and manage virtual servers. With EC2, you can easily provision and scale resources according to your needs. Remember to import your key pair to AWS to ensure secure access.


# public key
````
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCnTTam9QQfl4CPM2MfcJc4SnJufYkRaEKSo4bWP5Hj2a+dhaHd6b6FcvxalD3nQayyBa7qWYJh6N/mMKFCu5UBT7B03dECAj4wmrtn9UOKI87nBDj3X0Vct/Q8GlfQQS3h7YRLZeznSfReG/BSydGihRx8DI2Gy4WWHq1wbf+2fs0Caxk425pqHzZKHpJ5YkW8z7zetX/w6gzNJa1EkiaKKVXiR2Wu4MogWsoypYBNAWNIUtro10kjE7Kmjutp/kg6SeCBN0O5NQthOmYqxzcJl5nsCRCNPmfTzGokcaq/y1dTYOmnA6/5tUa1sM42jBMLZNwas17lnBjUNo+l+0wxq1GzRvaX8enhUg9UNQfMgIprPgEUkwsgBNv5NKcLVeSxVwo6HFpGM9AIrWgX3lmTrC4Ti9fmuDXARWNFX0Rw0VfGH1lh8nWOSR7x6k+LvaKWKvK7q9T7h2PeZ54bkk9xlykoCiYUsutssjxuxDM6SRZeQ6WE9JYaZUTPrEzYSovwMszgJXdwpkdFVc9rnrIu/HUNSW8ncPLQy/BOP06uWb2wHHELiz6V0dN2jDM0sK3CZUv5PGzjl1kN3fVvH7Vk8goBnVzXWH5nIW2mc+vlYumxETGLiAwMhlwviT/QwQeeXLSdZoFG9ffViC12GtQGQSn8nDoK84lOOgdEsl7E+Q== saide@SAIDEV
````


# private key

````
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY----
````````````````````


# firewalls: is nothing but security group: create allow-all sg

----------------------------------------

1. Create an instance.
2. Linux is not an operating system; it is a kernel.

# OS vs. Kernel

1. Kernel - connects to hardware; no utilities or shell included.
2. Linus Torvalds - creator of Linux.
3. Unix - very costly and tightly coupled to hardware.
4. Linux kernel - based on Unix principles but written from scratch in the C programming language.
5. Open source software.


1. kernal+package+shell =os
2. android is flovour of linux
3. kernal+packge+shell+ui

# ubuntu
desktop= kernal +shell+ui
server= kernal + shell
centos
rhel
fedora
suse
arch linux
99% same ==> few commands only will differ

RHEL== open sourse ==but not free
code open sourse -take the code

support --immediate call

community edition:
RHEL = centos =fedora=almalinux

RHEL = code =os centsos =internet community

============================================================
# connecting linux server
ip addrees
username =ec2-user
private-key

# ssh -i <path-to-private-key> username@ip
# ssh -i meen.pem ec2-user@ipaddress  
# using gitbash as client to connect server
# protocol = ssh  =22
# protocal = ip address port no


# absolutpath vs relative path



