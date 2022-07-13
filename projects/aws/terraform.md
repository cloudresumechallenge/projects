## CHALLENGE

Using any language you prefer, write code that creates an EC2 instance running a basic web application in Docker using a single command from the user.

* Before the script is run, there should be no EC2 instances running and afterward the script should output the address of your working web application.
* The single command from the user can (and likely will) call a longer shell script, or other configuration management code.
* The web application can be any common framework (Django, Rails, Symfony, etc.), but not the default Nginx or Apache setup.
* If needed, you can manually create pre-requisites such as SSH key pairs or other prerequisites.
* Create the terraform code around the inputs and outputs shown in this README
* Use public modules where possible to create DRY code (Don't Repeat Yourself) 

## NOTES

#### ASSUMPTIONS
ec2 ssh key already exists 

#### MODULES
This makes use of the following modules:
- terraform-aws-modules/elb/aws
- terraform-aws-modules/vpc/aws

#### BACKEND
Run a `terraform init && terraform apply` in remote_state_init to initialize a backend configuration and store state in s3. This does not do
any kind of state locking with DynamoDB or any other at the moment since this code is not meant for more than single use. 

Then run `terraform init -backend=true -backend-config=backend.tfvars` and you will be set to run `terraform apply -var-file=terraform.tfvars`

#### VPC 
This will create public and private subnets with VPC, with public subnet defined as "has a route to internet gateway," and private defined as 
"has a route to nat gateway." 

#### AUTO SCALE
Auto Scaling with the settings provided by default has a will take about 5 minutes or so to generate a scaling 
event, either up or down. To initiate a scaling event just add the tag key "PerfTest" with a value of "CPU" and a cron job on the instance will
run stress with a random value of --cpu=8 cores, which will quickly generate CPU load. To scale down simply remove the "PerfTest" key and the 
script will run a `pkill stress` thereby reducing CPU load. To receive SMS alerts simply add `phone_number="+15555555555"` with your phone number
substituted and you will receive an alert when auto scale launches a new instane, terminates an instance, or if there us a launch error

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| ami\_name |  | string | `"amzn-ami-hvm*"` | no |
| ami\_owner |  | string | `"amazon"` | no |
| asg\_size |  | string | `"t2.micro"` | no |
| bucket |  | string | `""` | no |
| bucket\_name |  | string | `"foo-bar-us-east-2"` | no |
| costcenter |  | string | `"foo@example.com"` | no |
| environment |  | string | `"dev"` | no |
| key |  | string | `"null.tfstate"` | no |
| key\_name |  | string | `"foobar"` | no |
| name |  | string | `"foo"` | no |
| phone\_number | Used for getting auto scale alerts | string | `"+15555555555"` | no |
| profile |  | string | `"foo"` | no |
| region |  | string | `"us-east-2"` | no |
| whitelist | IPs to whitelist for ssh access | list | `<list>` | no |

## Outputs

| Name | Description |
|------|-------------|
| elb\_dns |  |
| sg\_group\_ec2 |  |
| sg\_group\_elb |  |
