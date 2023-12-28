# AWS Project Using Terraform

## Create VPC
- Create a VPC.

## Create Subnets
- Create two subnets within the VPC:
  - One public subnet
  - One private subnet

## Enable Public IP on Launch
- Enable auto-assign public IPv4 address.

## Create Networking Components

- Create an Internet Gateway and attach it to the VPC.

## Configure Public Subnet
- Create a public route table.
- In the route section of the public route table, add the Internet Gateway.
- In the subnet association section, add the public subnet.

## Configure Private Subnet
- Create a NAT Gateway in the public subnet.

- Use the route table created during VPC creation.
- In the route section of the VPC route table, add the NAT Gateway.
- In the subnet association section, add the private subnet.

## Create Security Groups
1. **WebServer Security Group:**
   - Allow incoming traffic on ports 80 from the world and port 22 only from admin.

2. **Jump-Server Security Group:**
   - Allow incoming traffic on port 22 only from admin.

3. **RDS Server Security Group:**
   - Allow incoming traffic on port 3306 from the public subnet.
   - Allow incoming traffic on port 22 from the Jump Server.

## Create Network ACL (NACL)
- Attach the NACL to the public subnet.
- Open the ports specified in the associated Security Groups for instances in the public subnet.

## Launch Instances
1. **Launch WebServer:**
   - Launch a WebServer in the VPC's public subnet.
   - Apply the WebServer Security Group.

2. **Launch Jump Server:**
   - Launch a Jump Server in the VPC's public subnet.
   - Apply the Jump-Server Security Group.

3. **Launch RDS Server:**
   - Launch an RDS Server in the VPC's private subnet.
   - Apply the RDS Server Security Group.

