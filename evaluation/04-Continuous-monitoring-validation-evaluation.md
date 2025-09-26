Evaluation against Zero Trust Security Principles - Continuous Monitoring and validation

Method: The AWS CloudTrail keeps track of all these API calls, including both successful and failed logins, in the AWS account. And this works with AWS CloudWatch so that the events are transmitted in real time. 
There were several attempts to connect in to the AWS console using IAM. The CloudWatch alert goes off when the threshold is reached, but only for unsuccessful login attempts. This is because both failed and successful logins are logged. This alters the state of the CloudWatch alarm and causes the AWS Simple Notification Service (SNS) subject to send an alert email to all of its subscribers (in this case, the author's Gmail). The unsuccessful authentication was removed from the list of failed attempts, as indicated in the picture.   

Perform the below to evaluate this principles
1. Try to enter wrong password for admin and developer while logging in to console.
2. Create some users without MFA and try to access the services on AWS console.
3. All these failed and unauthorized actions will be logged in cloudtrail and send to cloudwatch.
4. If there are multiple logins in a minute for example (threshold set while configuring alarm), then the alarm is  
   triggered and which in turn triggers SNS to send emails to the subscriber.(You can add your email for testing).
5. This shows, that continuous monitoring and validation is successfully tested.


