# Hosting a Static Website on a Default AWS VPC

This repository documents the process of hosting a static website on AWS using the default network architecture. The project involves uploading web files to an S3 bucket and GitHub repository, then deploying them onto an EC2 instance using Bash scripts. Below are the detailed steps and resources utilized in this setup:

## Steps:

1. **Default VPC Configuration:**
   - Utilized the default VPC with DNS enabled, comprising public and private subnets across 2 availability zones for fault tolerance and high availability.

2. **Subnet Setup:**
   - Public subnet: Holds the Bastion Host and Nat Gateway.
   - Private subnet: Hosts the webserver.

3. **Networking Components:**
   - Utilized the default Internet Gateway and Route Table to route traffic to the VPC:
     - Public Route Table: Routes traffic from the Internet Gateway.
     - Private Route Table: Routes traffic from the NAT Gateway to the private subnet.

4. **NAT Gateway Creation:**
   - Created a NAT Gateway and launched it in the public subnet to facilitate traffic routing to the private subnet through the Route Table.

5. **Security Groups:**
   - Created Security Groups for secure access:
     - SSH (port 22) from specified source IP address.
     - HTTP (port 80) open to the world (0.0.0.0/0).
     - HTTPS (port 443) open to the world (0.0.0.0/0).

6. **S3 Bucket Setup:**
   - Created an S3 bucket and uploaded web files.
   - Configured bucket policy to allow public access for "GetObject" operation.

7. **EC2 Instance Launch:**
   - Launched an EC2 instance.

8. **Bash Script for S3 Deployment:**
   - Created a Bash script to download web files from the S3 bucket and host the HTML website on the EC2 instance.

   ```bash
   # AOS Notes Assignment1
   # S3 Script
   sudo su
   yum update -y
   yum install -y httpd
   cd /var/www/html
   wget https://sunski411.s3.amazonaws.com/mole+(1).zip
   unzip mole.zip
   cp -r mole-main/* /var/www/html
   rm -rf mole-main mole+(1).zip
   systemctl enable httpd
   systemctl start httpd
   ```

9. **GitHub Repository Setup:**
   - Created a repository in GitHub and uploaded the web files.

## Bash Script for GitHub Deployment:

```bash
# AOS Notes Assignment1
# GitHub Script
sudo su
yum update -y
yum install -y httpd
cd /var/www/html
wget https://github.com/sunski411/host-html-website-on-aws/archive/refs/heads/main.zip
unzip main.zip
cp -r host-html-website-on-aws-main/* /var/www/html
rm -rf host-html-website-on-aws-main main.zip
systemctl enable httpd
systemctl start httpd
```



