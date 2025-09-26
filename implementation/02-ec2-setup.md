
Launch an EC2 instance

First, create a security group. Go to AWS Console -> VPC service -> Security Groups

Create a Security Group

Go to VPC → Security Groups → Create security group.
Name: sg-web
VPC: my-vpc (the one created earlier)

In Inbound rules:
Add rule: SSH, Port 22, Source = 0.0.0.0/0
Add rule: HTTP, Port 80, Source = 0.0.0.0/0

Leave Outbound rules as default (all traffic allowed).

Create security group


Next, Launch an EC2 instance. Go to EC2 instances on the AWS Console.

1. Name: web-server.

2. AMI: Choose Amazon Linux 2 AMI (Amazon Linux AMI is deprecated, Amazon Linux 2 is recommended).

3. Instance type: e.g., t2.micro (free-tier eligible).

4. Network settings:
   VPC: my-vpc
   Subnet: public-subnet
   Auto-assign public IP: Enable
   Firewall (security group): Select existing → sg-web

5. Advanced details → User data: Paste the script:

#!/bin/bash
# Update packages
yum update -y

# Install Apache
yum install -y httpd

# Start Apache
systemctl start httpd
systemctl enable httpd

# Write your custom HTML
echo "This is my web application" > /var/www/html/index.html

6. Click on Launch Instance.

Once the instance is created, try to connect via EC2 connect. USe the public IP address of the server and access it from web browser.





