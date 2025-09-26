Evaluation against Zero Trust Principle - MFA

Method: AWS IAM users (admin and developer) were set up to need MFA to get in to the AWS console. This was done with two tests. The first test involved logging into the AWS console with valid credentials and a valid MFA token for both admin and developer accounts. The second test was to try to log in with just a password and no MFA token (another user was created to evaluate the second test).

Perform the below steps to evaluate - logging into the AWS console with valid credentials and a valid MFA token 
1. Login to the AWS console, as a admin or a developer user who has MFA enabled
2. Enter the username and password on the console
3. The next, enter the MFA token from your google authenticator app on phone
4. The login is successful, next switch role. On top right corner, click on profile and switch role.
5. If you have logged in as admin, you should be able to see the EC2 instances and not RDS database (As expected) and if you are developer, you should be able to see RDS and EC2 instances.
6. This confirms, only MFA enabled are able to see the resources or services permitted to them.

Perform the below steps to evaluate - logging into AWS console with just a password and no MFA token 
1. Login to the AWS console as a user who has no MFA enabled
2. Enter the username and password on the console.
3. The login will be successful but this user wont get to enter the MFA token as it is not enabled.
4. This user should not be able to view any services or resources on AWS console (as expected)

This test was successful.
