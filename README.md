# ZeroTrustSecurity-Cloud-UseCase

The Proof of Concept is built using a two-tier application architecture in one AWS region, which makes it easier to use and control. The study examines a web application deployed on an Amazon EC2 instance on a public subnet, which interfaces with an Amazon RDS database located in a private subnet. We adopted the two-tier idea on purpose because it is akin to a standard design used in the industry that strikes a balance between being simple and realistic. This kind of architecture shows how the Zero Trust Security framework operates in a safe and standard setting. The architecture makes it easy to add security by putting tight access controls between levels, dividing the network into sections, and keeping an eye on all interactions. AWS services that fit with Zero Trust ideas in the cloud environment, like Identity and Access Management (IAM), Multi-Factor Authentication (MFA), Virtual Private Cloud (VPC), CloudWatch monitoring, and CloudTrail, make this two-tier approach strong. 


## Technologies Used

AWS VPC – secure networking  
EC2 – compute resources  
RDS – database  
IAM with MFA – identity and access control  
CloudWatch + SNS – monitoring and alerts  

## How to Use

Clone this repo:
   bash
   git clone https://github.com/sgshilpa11/ZeroTrustSecurity-Cloud-UseCase.git
   cd zero-trust-cloud-poc

