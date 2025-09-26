VPC Configuration on AWS Console

The values are assumptions (change as you like):
VPC CIDR: 10.0.0.0/16 • Public Subnet: 10.0.1.0/24 • Private Subnet: 10.0.2.0/24 • Same AZ (e.g., us-east-1a)

Create the VPC

1. VPC → Create VPC → VPC only

Name: my-vpc • IPv4 CIDR: 10.0.0.0/16

2. After creation: select the VPC → Actions → Edit VPC settings → ensure DNS hostnames = ON (DNS resolution is on by default).

3. Create the subnets

   Subnets → Create subnet

   VPC: my-vpc

   Subnet 1: Name public-subnet, AZ us-east-1a, CIDR 10.0.1.0/24

   Subnet 2: Name private-subnet, AZ us-east-1a, CIDR 10.0.2.0/24

   Select public-subnet → Actions → Edit subnet settings → enable Auto-assign public IPv4 address.

4. Create and attach an Internet Gateway

   Internet Gateways → Create IGW → Name my-igw

   Select it → Actions → Attach to VPC → pick my-vpc.

5. Public route table (send default traffic to IGW)

   Route tables → Create route table → Name rtb-public → VPC my-vpc.

6. Select rtb-public → Routes → Edit routes → Add route:

   Destination: 0.0.0.0/0 → Target: Internet Gateway my-igw → Save.

7. Subnet associations → Edit subnet associations → check public-subnet → Save.

8. Private route table

   Route tables → Create route table → Name rtb-private → VPC my-vpc.

   Subnet associations → associate private-subnet.
