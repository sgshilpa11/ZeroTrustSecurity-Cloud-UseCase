EValuation against the Zero Trust Prinicple - Least Privilege

There are now two IAM users and their roles. One is a developer user with the role developer-ec2-rds-role, which only lets them read and write to the database but not delete it. The other is an admin user with the role admin-ec2-role, which only lets them access the web server on the ec2 instance and not the database. For both users, wide-ranging permissions were clearly refused. The controlled tests were done so that each user did things that were outside of their normal duties. For example, the developer user tried to shutdown the EC2 instance, while the admin user tried to access the database.

Perform the below steps for evaluation

1. Login to the AWS console as user admin.
2. Switch role - Go to profile on right corner and click on switch role
3. Go to EC2 service, the user admin should be able to access the EC2 instance
4. Go to RDS service, the user admin will not be able to access the RDS database -> unauthorized access

To check the logs,
1. Go to CloudTrail service -> Events -> down the CSV file
2. Another way to fetch the data, is to go to S3 service and the appropriate bucket and search date wise for the
   logs.

Check if the SNS notifications are sent to the subscribed email about the unauthorized access
