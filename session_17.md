It is possible to create resources using the command line interface without logging into the AWS Management Console. However, to access AWS services, authentication and authorization are essential. AWS utilizes roles, which are assigned specific permissions to define what actions can be performed and which resources can be accessed.
authentication means having username and password
Each user is assigned a specific role within the system, which defines their level of access and the permissions associated with that role. These permissions determine what actions the user can perform, including viewing, editing, and managing different resources or features based on their assigned role.
In AWS, each user is assigned specific permissions that vary based on the resources they are interacting with. These permissions dictate what actions a user can perform on different services and resources, such as S3 buckets, EC2 instances, or IAM roles. For example, one user may have full access to modify and delete EC2 instances, while another user may only have read access to S3 buckets. This tailored approach ensures that users have the appropriate level of access needed for their roles, enhancing security and management of resources within the AWS ecosystem.
In AWS resources should have the access to access another resources


# roles for AWS resources:
#lab:
1. create role for ec2 resourse
2. if we give full access to Ec2 it will create another instances
3. `aws ec2 run-instances --image-id ami-123456 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-123456` = this is the command to create ec2 instance but for that we need to configure was

# AWS User Configuration and EC2 Management

## Configuring an IAM User

1. **Create an IAM User**: Begin by creating a new IAM (Identity and Access Management) user in the AWS Management Console. This user will be used for managing AWS resources securely.

2. **Assign Administrator Access**: During the user creation process, grant the user administrative access by attaching the "AdministratorAccess" policy. This will allow the user to perform all actions across all AWS services.

3. **Generate Access Keys**:
   - Navigate to the user’s security credentials page.
   - Locate the option to create access keys. Select “Create access key.”
   - Follow the prompts to generate the access keys for Command Line Interface (CLI) usage. Once you go through the checklist, click ‘Next’ and then ‘Create access key’.
   
4. **Record the Access Keys**: After the keys are created, you will receive an **Access Key ID** and a **Secret Access Key**. Ensure to copy these values and store them securely as they will be needed for future CLI configurations.

  # Example of Access Key: `AKIAQZFG5BLL5KL7OYYA`
  # Example of Secret Key: `3POvEElQAC8meEh/OgXlsH+yRm4Pum5xXHIkZYmf`

5. **Configure AWS CLI**: When you run the command `aws configure` in your CLI, it will prompt you to enter the **Access Key ID** and the **Secret Access Key**. These credentials are stored in your user home directory in the hidden folder `.aws/`. You can check this by executing the command `ls -la ~/.aws/`.

## Security Consideration for EC2 Instances
It is important to note that storing access keys directly on an EC2 instance poses a security risk, as anyone gaining access to the instance can potentially use these keys. To enhance security:

1. **Delete Access Keys**: If you've used IAM users and keys, it’s advisable to delete the access keys and the IAM user itself once they are no longer needed.

2. **Use IAM Roles for EC2 Instances**: Instead of using access keys, create an IAM role specifically for EC2 resources:
   - **Create a Role**: Set up a new role in IAM, granting it permissions that are necessary for the tasks the EC2 instances will perform.
   - **Attach the Role to an EC2 Instance**: To attach the created role to an EC2 instance, navigate to the instance in the AWS console, then go to **Actions > Security > Modify IAM Role**. From there, select the IAM role you created and click **Update IAM Role**.

## Launching EC2 Instances

### Instance Creation Command
To launch a new EC2 instance from the CLI, you can use the following command, where you need to replace `379183` with the appropriate identifier for your AMI (Amazon Machine Image):

```bash
aws ec2 run-instances --image-id ami-0b4f379183e5706b9 --instance-type t2.micro --security-group-ids sg-02cfa8ece2d41bfd1
```

### Creating Multiple Instances and Records
If you want to launch multiple instances simultaneously and keep a record of the process, follow these steps:

1. **Create a Script for Instance Creation**: Write a script, e.g., `roboshop.sh`, that contains the necessary commands for launching instances. Include the AMI ID and security group ID within the script for easy management.

2. **Example Script**: The `roboshop.sh` file can include commands like the one above, tailored for your needs.

By following these detailed steps, you can securely manage AWS users and efficiently launch EC2 instances while adhering to best practices in security and resource management.

There are two primary methods for creating EC2 instances through the Command Line Interface (CLI). 

The first method involves configuring a user with the necessary permissions. While this approach is straightforward, it has its drawbacks; specifically, EC2 instances may require access keys and secret keys to authenticate API requests. This means that if these credentials are stored on the instance itself, they could be exposed, leading to potential security vulnerabilities.

The second method involves assigning appropriate IAM roles to the EC2 instances. This approach is generally considered more secure because it eliminates the need for access keys and secret keys to be stored directly on the instance. Instead, the IAM role provides temporary security credentials for API requests. Because these credentials are handled and rotated automatically by AWS, this method significantly reduces the risk of unauthorized access and is therefore recommended as the best practice for managing permissions on EC2 instances. 

Overall, while both methods can effectively create EC2 instances, using IAM roles enhances security and streamlines access management.

#vscode
#!/bin/bash
AMI=ami-0b4f379183e5706b9
SG_ID=sg-02cfa8ece2d41bfd1

INSTANCES=("mongodb" "redis" "mysql" "rabbitmq" "catalogue" "user" 
"cart" "shipping" "payment" "dispatch" "web")
for i in "${INSTANCES[@]}"
do 
   if [ $i == "mongodb" ] ||  [ $i == "mysql" ] ||  [ $i == "shipping" ]
   then
      INSTANCE_TYPE="t3.small"
    else
      INSTANCE_TYPE="t2.micro" 
    fi

    aws ec2 run-instances --image-id ami-0b4f379183e5706b9 --instance-type $INSTANCE_TYPE 
    --security-group-ids sg-02cfa8ece2d41bfd1
done
the above is shellscript is to create ec2 instance at a time using for loop
we need ip adrees to create records
#!/bin/bash
AMI=ami-0b4f379183e5706b9
SG_ID=sg-02cfa8ece2d41bfd1

INSTANCES=("mongodb" "redis" "mysql" "rabbitmq" "catalogue" "user" 
"cart" "shipping" "payment" "dispatch" "web")
for i in "${INSTANCES[@]}"
do 
  
   if [ $i == "mongodb" ] ||  [ $i == "mysql" ] ||  [ $i == "shipping" ]
   then
      INSTANCE_TYPE="t3.small"
    else
      INSTANCE_TYPE="t2.micro" 
    fi

    
    IP_ADDRESS=$(aws ec2 run-instances --image-id $AMI --instance-type $INSTANCE_TYPE --security-group-ids $SG_ID --tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value=$i}]" --query 'Instances[0].PrivateIpAddress' --output text)
    echo "$i: $IP_ADDRESS"
done
# aws route53 command to create record shell script
aws route53 change-resource-record-sets \
  --hosted-zone-id 1234567890ABC \
  --change-batch '
  {
    "Comment": "Testing creating a record set"
    ,"Changes": [{
      "Action"              : "CREATE"
      ,"ResourceRecordSet"  : {
        "Name"              : "'" $ENV "'.company.com"
        ,"Type"             : "CNAME"
        ,"TTL"              : 120
        ,"ResourceRecords"  : [{
            "Value"         : "'" $DNS "'"
        }]
      }
    }]
  }
  '
