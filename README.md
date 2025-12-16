# Deploying-Node.js-application-on-AWS-


##  Overview
This project demonstrates how to deploy a **Node.js–based web application** on AWS using a secure and production-style architecture.

- The application runs on **EC2 instances in private subnets** and is exposed to users through an **internet-facing Application Load Balancer (ALB)**.
- A **PostgreSQL database hosted on Amazon RDS** is used for persistence, and **Amazon S3** is used for static assets.
- The focus of this project is **infrastructure design, networking, and security**, rather than application development.

---

##  Architecture Overview
The Node.js application is deployed using a **multi-tier AWS VPC architecture**:

- **Custom VPC** with public and private subnets  
- **Application Load Balancer** in public subnets  
- **Node.js application** running on EC2 instances in private subnets  
- **Amazon RDS (PostgreSQL)** in a private subnet  
- **NAT Gateway** for outbound internet access  
- **Security group–based traffic control**  



<img width="602" height="601" alt="VPC drawio" src="https://github.com/user-attachments/assets/d578e054-6545-4674-a999-4e0963c449cf" />


##  AWS Services Used
- **Amazon VPC** – Network isolation and routing  
- **Amazon EC2** – Hosts the Node.js application  
- **Application Load Balancer (ALB)** – Routes user traffic to EC2 instances  
- **Amazon RDS (PostgreSQL)** – Database backend  
- **Amazon S3** – Static asset storage  
- **NAT Gateway** – Allows private EC2 instances outbound internet access  
- **AWS Systems Manager (SSM)** – Secure access to EC2 without SSH  

---

## Application Deployment Flow
1. Users access the application using the **ALB DNS endpoint**.  
2. The **ALB**, deployed in public subnets, receives incoming HTTP traffic.  
3. Requests are forwarded to **EC2 instances** running the Node.js application in private subnets.  
4. The Node.js application:  
   - Connects to **Amazon RDS (PostgreSQL)** for data operations  
   - Retrieves static content from **Amazon S3**  
5. Outbound traffic from EC2 (package installs, updates) flows through the **NAT Gateway**.  

---

##  Security Implementation
- EC2 instances **do not have public IP addresses**  
- RDS database is **not publicly accessible**  
- Only the **ALB is exposed to the internet**  
- Security groups enforce **least-privilege access**:  
  - ALB → EC2 (application port)  
  - EC2 → RDS (PostgreSQL port)  
- No SSH access; EC2 instances are managed using **AWS Systems Manager**  

###  Screenshots to Attach
- ALB target group showing **Healthy status**  
- EC2 instances running in **private subnets**  
- RDS configuration showing **Not publicly accessible**  
- Security group inbound rules  
- SSM session access to EC2  

---

## Future Improvements
- Add **Auto Scaling Group** for EC2 instances  
- Enable **HTTPS using ACM**  
- Configure **RDS Multi-AZ**  
- Store secrets using **AWS Systems Manager Parameter Store** 
