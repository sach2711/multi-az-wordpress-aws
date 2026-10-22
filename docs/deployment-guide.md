# Deployment Guide: WordPress on AWS

## 1. Introduction

In this project, I deployed a WordPress website using AWS services. My main aim was to understand how a website can run on two EC2 instances and how a load balancer distributes requests between them.

I also connected WordPress to an Amazon RDS MySQL database. While setting up the project, I worked with AWS networking, security groups, server configuration, and database connectivity.

## 2. Setting Up the Network

First, I created a VPC for the project and configured public and private subnets.

I attached an Internet Gateway and configured the public route table so that internet traffic could reach the public-facing resources. I also configured security groups to control which components could communicate with each other.

The database was kept private and was not directly accessible from the public internet.

## 3. Configuring the EC2 Instances

I launched two EC2 instances to host the web application.

I installed Apache and PHP on the instances and configured the required files for WordPress. I also used AWS Systems Manager Session Manager to access the server terminal and run the required commands.

During this stage, I had to check the web server status and resolve configuration issues before moving to the next step.

## 4. Setting Up the Application Load Balancer

Next, I created an internet-facing Application Load Balancer and configured a target group for the two EC2 instances.

I registered both instances with the target group and configured the health checks. The load balancer receives requests from users and forwards them to healthy registered targets.

I then accessed the website through the ALB's DNS address instead of using an individual EC2 instance address.

## 5. Configuring Amazon RDS

I created an Amazon RDS MySQL database and configured its security group to allow database connections from the web-server security group.

I created a database for the application and checked the connection from the EC2 environment. I also verified that the application could retrieve a test message from the database.

After confirming the connection, I configured WordPress to use the RDS database.

## 6. Installing WordPress

I downloaded the WordPress package, extracted the files, and copied them into the Apache web directory.

I configured the WordPress database settings and opened the installation page through the load balancer. After completing the installation, I logged in to the WordPress administrator dashboard.

I then checked that the website was accessible through the ALB.

## 7. Testing the Project

I performed the following checks during implementation:

- Confirmed that the WordPress administrator dashboard opened successfully.
- Checked the connection between the web application and RDS.
- Verified that both EC2 instances were healthy targets in the target group.
- Opened the website using the load balancer's DNS address.

These checks helped me understand how the web servers, load balancer, and database work together.

## 8. Current Limitations

The web tier has two EC2 instances behind the Application Load Balancer. However, the RDS database is currently configured as Single-AZ.

RDS Multi-AZ deployment and automatic database failover have not been configured or tested. I would like to explore these features as a future improvement.

I also plan to test the application by stopping one web server at a time and checking whether requests continue to reach the remaining healthy server.

## 9. Conclusion

This project gave me practical experience with AWS EC2, Application Load Balancer, Amazon RDS, VPC, security groups, PHP, and WordPress.

I learned how to configure the individual services, connect them together, and troubleshoot problems during deployment. It also helped me understand why load balancing and database availability are important when hosting a web application.
