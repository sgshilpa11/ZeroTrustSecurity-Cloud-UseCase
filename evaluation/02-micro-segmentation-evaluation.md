Evaluation against the Zero Trust Principle - Micro-Segmentation

Micro-segmentation is used to control communication between the webserver and database tiers. This was done by splitting the Virtual Private Cloud (VPC) into a public subnet (where the EC2 webserver is housed) and a private subnet (where the RDS database is hosted). The AWS EC2 security group let HTTP and SSH traffic come in from the internet, but the AWS RDS security group only let MySQL traffic come in from the AWS EC2 security group on port 3306. This architecture reduced the attack surface by blocking direct internet or unauthorized VPC access to the database. This was done by not having any other incoming or outgoing restrictions. To assess this, two tests were performed: the first involved connecting to the RDS database using the endpoint from an EC2 instance within the same VPC, and the second involved connecting to the RDS database from an external source (the internet).


Perform below steps to evaluate: connecting to the RDS database using the endpoint from an EC2 instance
1. Login to EC2 instance 
2. Run this command to see if RDS Database is accessible from EC2.
   mysql -h rds-endpoint -P 3306 -u username -p password
   To get the endpoint of RDS, Go to RDS service and click on the RDS created and under connectivity and security  
   tab, the endpoint will be mentioned.
3. The RDS should be accessible from the instance and get a MySQL command prompt.

Perform below steps to evaluate: connecting to the RDS database from an external source (the internet)
1. Install MySQL server on your local machine.
2. Enter the command - mysql -h rds-endpoint -P 3306 -u username -p password
3. This test should fail because RDS does not allow external sources to connect as it does not have a public ip.

