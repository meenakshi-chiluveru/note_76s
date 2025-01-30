terraform.tfvars: it is a file to override default values of variables.tf
other wise we can give values in command line like 
terraform plan -var="instance_type=t3.medium"
when we declare variable values in variables.tf and terraform.tfvars and commandline the first preference goes to commandline always and second preference goes to terraform.tfvars
we can create .tfvars with different name = roboshop.tfvars
terraform plan -var-file="roboshop.tfvars"
first command line
second -var-file
terraform.tfvars
env variables

conditions:
Roboshop lo Web component costs?

if(expression){
	if true this will run
}

if(expression){
	if true this will run
}
else{
	if false this will run
}

expression ? "this will run if true" : "this will run if false"
