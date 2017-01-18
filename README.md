Go to live! kata
==================================

README 

In order to automate and provision the infrastructure requested by the XPeppers exercise, I have used AWS Cloudformation as the tool.
I tested it in my AWS account (for security purposes, an existing .PEM certificate has been used to access via SSH the instance). 

I customized a Multi-AZ Wordpress template to provide availability, reliability and scalability for the deployment of an application.
With the term "application" I refer to the Wordpress platform, clean and ready to initiate (the first step is to insert username, site title and then invent a password). 
You can find the URL link, as generated from the execution of the AWS CloudFormation template, in Outputs file in the aws_outputs folder.

The template used is in the aws_cloudformation folder.



The architecture is composed from:

1 ELB (name: XpeppersS-ElasticL-4DEM1BHAMS3N) available in 3 Availability Zones, which actually points to the Apache (httpd) Webserver (XpeppersStack-Test).

3 subnets (one for each AZ)

1 instance t2.micro which is the Webserver (name: XpeppersStack-Test), accessible from TCP HTTP port 80 and via TCP SSH with the key consoft_pair.pem
Webserver is supported from an AutoScaling Configuration (min 1 and max 5 instances, of type t2.micro, in case EC2 healthchecks fail). It assures that a minimum of 1 instance is always ON (no AutoScaling policy applied) and lauched automatically. The new instances respects the Webserver security group settings in the default VPC.

1 DB instance of type MySQL (of type m1.small for exercise purpose) in a security group (inbound accepts connection via TCP, port 3306, ESCLUSIVELY from the Webserver(s)). You can connect to the db instance via any client installed in the Webserver.