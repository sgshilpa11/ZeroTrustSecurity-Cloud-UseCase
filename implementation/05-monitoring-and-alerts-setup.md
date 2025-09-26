Setup CloudTrail, CloudWatch and SNS for alerts

AWS CloudTrail
Go to AWS console -> AWS ClouldTrail -> Create a trail
1.Trail name: test-security-cloudtrail
2.Choose create new s3 bucket and leave the name as default
3.Under Additional settings 
  Enable log file validation
  SNS notification delivery -> Create new SNS Topic
4.Enable CloudWatch logs -> Create new log group
5.Events -> Choose Management events
6.Click on create

Next, Click on CloudWatch Service
1.Go to LogGroups 
2.Create a metric filter name- Unauthorizedactions
3.Enter the Filter pattern - "Unauthorized"
4.Assign a metric and review and create

Next, Go to Alarms under CloudWatch
1.Create Alarm
2.select the metric filter created in above step and enter details like period and conditions
3.Click next and configure the SNS settings and click create

Next, Go to AWS SNS service
Click on create subscription and select the topic
And select email and enter the email address which should receive the notifications.


 
