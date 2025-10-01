

---

# Static Website Hosting on AWS - DevOps Project

This project showcases a static HTML web application hosted on AWS. The deployment utilized various AWS services to ensure scalability, fault tolerance, and security. The architecture comprises public and private subnets across multiple Availability Zones, leveraging AWS networking, compute, and security features.

## Project Overview

In this project, I hosted a static website on AWS using an EC2 instance. Below is an outline of the AWS resources and configurations used.

### AWS Architecture

1. **VPC Configuration**: Set up a Virtual Private Cloud (VPC) with both public and private subnets distributed across two Availability Zones.
2. **Internet Gateway**: Configured to enable connectivity between the VPC instances and the wider internet.
3. **Security Groups**: Used as network firewalls to control inbound and outbound traffic to resources within the VPC.
4. **High Availability**: Employed two Availability Zones to ensure reliability and fault tolerance.
5. **Subnet Configuration**:
   - Public Subnets for resources such as NAT Gateway and Application Load Balancer.
   - Private Subnets to host web servers (EC2 instances) for added security.
6. **NAT Gateway**: Allowed instances in private subnets to access the internet without exposing them to public traffic.
7. **EC2 Instance Connect Endpoint**: Enabled secure connections to instances within public and private subnets.
8. **Launch Template**: Used a Launch Template to define instance configurations for Auto Scaling.
9. **Application Load Balancer**: Distributed incoming web traffic evenly across an Auto Scaling Group of EC2 instances in multiple Availability Zones.
10. **Auto Scaling Group**: Managed EC2 instances dynamically to ensure availability, scalability, and fault tolerance.
11. **Certificate Manager**: Secured application communications.
12. **SNS Notifications**: Configured to monitor Auto Scaling Group activities.
13. **Route 53**: Managed the DNS record and domain name registration for the website.

### Deployment Steps

1. **Install and Configure Apache HTTP Server**:
   - Updated installed packages.
   - Installed and configured Apache as the web server.
   - Set up Apache to serve content at system boot.

2. **Clone Repository and Deploy Website**:
   - Installed Git to clone the project repository.
   - Deployed web files to the Apache root directory from the GitHub repository.

3. **Enable Continuous Availability**:
   - Configured Auto Scaling and Load Balancing to ensure the site’s reliability and responsiveness.

### Deployment Script

The following script was used for configuring the EC2 instance to host the website:

```bash
#!/bin/bash
# Switch to the root user
sudo su
# Update all installed packages
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change directory to Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project repository
git clone https://github.com/michealL682/host-a-static-website-on-aws.git
# Copy files to Apache root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Clean up by removing the cloned directory
rm -rf host-a-static-website-on-aws
# Enable and start Apache
systemctl enable httpd
systemctl start httpd
```

### Project Files

The project repository contains:
- **Reference Diagrams**: Illustrates the AWS architecture.
- **Deployment Scripts**: Bash scripts used for EC2 configuration and website deployment.

### Features

- **Scalability**: Auto Scaling Group dynamically manages EC2 instances.
- **Fault Tolerance**: Resources deployed across multiple Availability Zones.
- **Enhanced Security**: Web servers in private subnets with controlled internet access.
- **Monitoring and Alerts**: SNS configured for notifications on Auto Scaling Group activities.

## Getting Started

1. Clone this repository.
2. Configure AWS resources following the architecture provided.
3. Deploy using the provided script or customize it as needed.

---


