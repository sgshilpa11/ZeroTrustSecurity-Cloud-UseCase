Steps to create AWS RDS instance - Single AZ deployment for the test purpose

Already have a VPC with public + private subnet and an EC2 in the public subnet (Apache + SSH access).
Now create an Amazon RDS MySQL database in the private subnet (free tier, single AZ).
Then configure security groups so that only your EC2 can connect to RDS


1. Create a Security Group for RDS

Go to VPC → Security Groups → Create security group.
Name: sg-rds
VPC: my-vpc
In Inbound rules:
Add rule: MySQL/Aurora (3306) → Source = sg-web (your EC2’s SG).
(This ensures only EC2 in sg-web can connect.)
Outbound rules: leave as default (all).

2. Create a Subnet Group for RDS

RDS needs a DB subnet group spanning at least two subnets. Since there is a private subnet, there is a need of another (same region, different AZ) — even if you choose Single-AZ deployment.

Create another subnet (e.g., 10.0.3.0/24) in private AZ us-east-1b.
Name: private-subnet-2.
Associate it with the private route table.
Go to RDS → Subnet groups → Create DB Subnet Group.
Name: my-db-subnet-group
VPC: my-vpc
Add both private subnets (private-subnet in 1a and private-subnet-2 in 1b).

3. Create the RDS Database

a.Go to RDS → Databases → Create database.

b.Engine: MySQL.

c.Templates: Free tier.

d.DB instance identifier: mydb.

e.Master username: db-user.
  Master password: create one.

f.DB instance size: db.t3.micro (free-tier eligible).

g.Storage: default 20 GiB (gp2, free).

h.Connectivity:
  VPC: my-vpc
  Subnet group: my-db-subnet-group
  Public access: No (keeps DB private)
  VPC security group: select sg-rds
  Availability: Single AZ

i.Additional settings:
  Initial DB name: myappdb (optional).

Create database. This will take few minutes. Once it is ready, you can see status = Available.

##Verify the connect from EC2 instance to RDS##

1.Go to EC2 connect on the AWS Console.
2.Enter the below command. 
  mysql -h <RDS_ENDPOINT> -u db-user -p providepassword
3.If success, you get the MySQL prompt (mysql>)


