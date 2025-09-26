
Here, Lets create two users - admin and a developer and enable MFA for both users.



Create the IAM Users

1.Go to the AWS Management Console → IAM → Users → Add users.
2.Enter a username: admin
3.Select Provide access to AWS Management Console
4.Set a password (custom)
5.Skip all and click on create
6.Repeat steps from 1 to 5 to create next user developer.


Enable MFA for the IAM Users

DO the below steps for both the users - admin and developer. Each user must sign in to perform below.

1.Go to IAM → Users → <username> → Security credentials.
2.Under Multi-factor authentication (MFA) → Click Assign MFA device.
3.Select Authenticator app → Continue.
4.Open Google Authenticator (or another TOTP app) on your phone.
5.Choose Add account → Scan QR code.
6.Scan the QR code shown in AWS console.
7.Enter the two consecutive MFA codes from your app → Submit.
  Now MFA is enabled for that IAM users

Verify

1.Sign in again as that IAM user - admin or developer
2.After entering username + password, AWS prompts for MFA code.
3.Enter the code from Google Authenticator → access granted.

