Create two roles that trusts IAM users (admin and developer) to grant specific permissions.

First, create the role for user admin

1.Go to IAM → Roles → Create role.
2.Trusted entity type:
  Choose AWS account.
  Select This account (same AWS account as the user admin)
3.Click Next and create a permissions policies by adding below json code. This will allow user admin to access   
  ready only EC2 instances and deny permissions for RDS database and other services as required for the use-case.
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EC2ReadOnly",
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*"
            ],
            "Resource": "*"
        },
        {
            "Sid": "EICConnectOnly",
            "Effect": "Allow",
            "Action": [
                "ec2-instance-connect:SendSSHPublicKey"
            ],
            "Resource": "arn:aws:ec2:*:*:instance/*",
            "Condition": {
                "StringEquals": {
                    "ec2:osuser": "ec2-user"
                }
            }
        },
        {
            "Sid": "ExplicitDenyRDSControlPlane",
            "Effect": "Deny",
            "Action": "rds:*",
            "Resource": "*"
        },
        {
            "Sid": "ExplicitDenyRDSIAMAuth",
            "Effect": "Deny",
            "Action": "rds-db:connect",
            "Resource": "arn:aws:rds:us-east-1:accoundid:db:rds-test-database/db_user"
        }
    ]
}

4.Name the role (admin-ec2-role) and create it.
5.Once the role is created, add the below trust policy under Trust Relationships Tab of this role.
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::accountod:user/admin"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "Bool": {
                    "aws:MultiFactorAuthPresent": "true"
                }
            }
        }
    ]
}


Create two roles that trusts IAM users (admin and developer) to grant specific permissions.

Repeat the steps for user developer.

1.Go to IAM → Roles → Create role.
2.Trusted entity type:
  Choose AWS account.
  Select This account (same AWS account as the user developer)
3.Click Next and create a permissions policies by adding below json code. This will allow user developer to access
  ready only EC2 instances and read and write permissions for RDS database as required for the use-case.
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EC2ReadOnly",
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*"
            ],
            "Resource": "*"
        },
        {
            "Sid": "EICConnectOnly",
            "Effect": "Allow",
            "Action": [
                "ec2-instance-connect:SendSSHPublicKey"
            ],
            "Resource": "arn:aws:ec2:*:*:instance/*",
            "Condition": {
                "StringEquals": {
                    "ec2:osuser": "ec2-user"
                }
            }
        },
        {
            "Sid": "RDSDescribeForEndpoints",
            "Effect": "Allow",
            "Action": [
                "rds:DescribeDBInstances",
                "rds:DescribeDBClusters"
            ],
            "Resource": "*"
        },
        {
            "Sid": "AllowRDSIAMAuth",
            "Effect": "Allow",
            "Action": "rds-db:connect",
            "Resource": [
                "arn:aws:rds-db:us-east-1:accoundid:dbuser:db-ZXMJNP7SETUT7SM25CLOOQRAQU/dba_user"
            ]
        }
    ]
}

4.Name the role (developer-ec2-rds-role) and create it.
5.Once the role is created, add the below trust policy under Trust Relationships Tab of this role.
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::accountid:user/developer"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "Bool": {
                    "aws:MultiFactorAuthPresent": "true"
                }
            }
        }
    ]
}


Next, the users admin and developer have to assume these roles. Do the below steps
1.Go to users, click on admin user and permissions tab and add the below code as inline policy
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAssumeAdminshilRole",
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::accountid:role/admin-EC2-role",
            "Condition": {
                "Bool": {
                    "aws:MultiFactorAuthPresent": "true"
                }
            }
        }
    ]
}
2.do the same for developer as well and add below code
   {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAssumeAdminshilRole",
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::accountid:role/developer-ec2-rds-role",
            "Condition": {
                "Bool": {
                    "aws:MultiFactorAuthPresent": "true"
                }
            }
        }
    ]
}

Now, both the users can use the assume roles to access the allowed resources.






