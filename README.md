# 🚀 Highly Available Web Application using EC2 Auto Scaling & ALB

## 📌 Project Overview

This project demonstrates how to deploy a **highly available, fault-tolerant, and auto-scalable web application** on AWS using industry-standard architecture.

Instead of running the application on a single EC2 instance (which is risky), this setup distributes traffic across multiple servers and automatically scales based on demand.

This is a **production-style cloud architecture** commonly used by real companies.

---

## 🎯 Aim

To build a resilient web application infrastructure that:

* Remains available even if one server fails
* Automatically scales based on traffic
* Distributes user requests efficiently
* Follows AWS best practices
* Demonstrates real DevOps and cloud skills

---

## 🏁 Final Outcome

After completing this project:

✅ Multiple EC2 instances run across Availability Zones
✅ Application Load Balancer distributes traffic
✅ Auto Scaling Group maintains desired capacity
✅ Failed instances are automatically replaced
✅ Infrastructure is production-ready

---

## 🧠 Architecture Flow

**User → Application Load Balancer → Target Group → Auto Scaling Group → EC2 Instances**

### Step-by-Step Flow

1. User opens the application URL
2. Request reaches the Application Load Balancer
3. ALB checks for healthy EC2 instances
4. Traffic is forwarded to one healthy instance
5. EC2 processes the request and sends response
6. Auto Scaling monitors load and adjusts capacity

---

# 🏗️ Architecture Diagram

<img width="1536" height="1024" alt="Highly Available WebApp" src="https://github.com/user-attachments/assets/1fe93c88-e5ed-41e3-a9a7-276392cdb717" />

---

# 🔧 AWS Services Used

## 🖥️ Amazon EC2

### Purpose

EC2 instances host the web application.

### What We Configured

* Amazon Linux / Ubuntu instance
* Apache web server
* Custom index.html
* Security group attached

### Why It Matters

EC2 provides the actual compute power where the application runs.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 212950" src="https://github.com/user-attachments/assets/2056ad7a-f02e-4678-8d35-6d5e23a3a0cd" />


---

## ⚖️ Application Load Balancer (ALB)

### Purpose

Distributes incoming user traffic across multiple EC2 instances.

### Key Features Used

* Internet-facing load balancer
* HTTP listener (port 80)
* Health checks
* Target group attachment

### Why It Matters

Without ALB:

* One server gets overloaded
* No fault tolerance
* Poor availability

With ALB:

* Traffic is evenly distributed
* Only healthy servers receive traffic
* Application stays highly available

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 214022" src="https://github.com/user-attachments/assets/3c17c13a-1444-4d4a-baa0-75f336d22693" />


---

## 🎯 Target Group

### Purpose

Acts as a bridge between ALB and EC2 instances.

### What It Does

* Registers EC2 instances
* Performs health checks
* Routes traffic only to healthy instances

### Health Check Configuration

* Protocol: HTTP
* Path: `/`
* Port: traffic port

### Why It Matters

This is why you saw the **503 error earlier** — when no targets are healthy, ALB cannot route traffic.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 214127" src="https://github.com/user-attachments/assets/bd1d1732-114c-4ff3-bc43-d21e9e0cf098" />


---

## 📈 Auto Scaling Group (ASG)

### Purpose

Automatically maintains and scales EC2 instances.

### Configuration Used

* Desired capacity: 2
* Minimum capacity: 2
* Maximum capacity: 4
* Multi-AZ deployment
* Attached to ALB target group

### What ASG Handles Automatically

✅ Launches new instances
✅ Terminates extra instances
✅ Replaces unhealthy instances
✅ Maintains high availability

### Why It Matters

This removes manual server management and enables true cloud scalability.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 214221" src="https://github.com/user-attachments/assets/27f9047f-fb6a-4906-a8cd-1e1e931e34af" />


---

## 🧩 Launch Template

### Purpose

Defines how new EC2 instances should be created.

### Key Settings

* Selected AMI
* Instance type (t2.micro)
* Security group
* Key pair

### Why It Matters

Ensures every new instance created by ASG is identical and properly configured.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 214315" src="https://github.com/user-attachments/assets/0aa3f91d-ef70-4f94-9d3c-f10195ef2111" />


---

## 🔐 Security Groups

### ALB Security Group

Allowed:

* HTTP (80) from anywhere

### EC2 Security Group

Allowed:

* HTTP (80) from ALB only
* SSH (22) from my IP

### Why This Is Important

This follows **least-privilege security**, which is expected in production environments.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 214406" src="https://github.com/user-attachments/assets/5333ec69-b227-4b25-9060-8b231ce37af4" />


---

# 🧪 Testing Performed

## ✅ Load Balancing Test

* Accessed ALB DNS
* Refreshed multiple times
* Observed traffic hitting different instances

## ✅ High Availability Test

* Verified instances in multiple AZs
* Confirmed ALB health checks

## ✅ Auto Scaling Test

* Configured scaling policy
* Observed automatic instance behavior

---

# 🚨 Issue Faced & Fix (Real Learning)

## Problem

Got **503 Service Temporarily Unavailable**.

## Root Cause

ALB had **no healthy targets** due to:

* Web server not running initially
* Health check failures

## Fix

* Started Apache service
* Verified security groups
* Confirmed health check path

✅ After fix, targets became healthy.

---

# 🎓 Key Learnings

From this project I learned:

* High availability architecture
* Load balancing concepts
* Auto Scaling behavior
* Health check importance
* Launch template usage
* Multi-AZ deployment
* AWS networking best practices
* Real production troubleshooting

---

# 🚀 Real-World Value

This architecture is used in:

* E-commerce platforms
* Banking applications
* SaaS products
* High-traffic websites

It demonstrates **job-ready AWS skills**.

---

# 🔮 Future Improvements

* Add HTTPS using ACM
* Move EC2 to private subnets
* Add NAT Gateway
* Implement CloudWatch scaling policies
* Add AWS WAF protection
* Implement CI/CD pipeline

---

## 👨‍💻 Author

**Sudarshan Mane**
Aspiring AWS & DevOps Engineer
Focused on building scalable and production-ready cloud architectures.

---

