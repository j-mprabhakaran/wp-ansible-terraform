#
#
# Deploying Wordpress blog on AWS using Terraform and Ansible

This code will help to create a 3 tier AWS environment containing Dev server, Highly available Production servers behind ELB in ASG, Highly available RDS database (Primary and Failover)

#
#
### Pre-requisites:

Local machine with Python, pip, AWS CLI, Ansible, Terraform installed. Refer instructions below for Ubuntu and MacOS. 

<script src="https://gist.github.com/jmprabhakaran/a3def7bacde998c3c2d3bdca8f69e2a9.js"></script>

Domain name for deploying the website

### IAM Setup: 
Create a terraform user for deploying the wordpress blog using terraform and provide administrator access (only Programmatic access)

### Domain Setup:

Run the below command to create delegation set which is required for setting up Route 53 records at the time of Terraform apply.

aws route53 create-reusable-delegation-set --caller-reference 1224 --profile name_of_aws_profile_configured_with_aws_credentials

Update the Nameserver of your domain using the NS output from above command.

### Execution

Change directory to the project directory.

run "terraform init" to initialize and download required plugins.

run "terraform plan" to review the list of AWS resources created by terraform.

run "terraform apply" to provision the infrastructure.

run "ansible-playbook -i aws_hosts s3update.yml" to copy the wordpress content from dev server to S3 bucket created by Terraform.
