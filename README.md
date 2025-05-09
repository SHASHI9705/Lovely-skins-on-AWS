# Lovely Skins – Secure 3-Tier AWS Architecture Deployment

**Lovely Skins** is an AI-powered web application that provides users with skincare suggestions based on uploaded skin images. This project is deployed on AWS using a robust and scalable **3-tier architecture** that ensures high availability, security, and performance.

---

## 🌟 Project Summary

- 🔬 AI-driven skin analysis (using static pre-trained models).
- 🛡️ Data privacy ensured – no user data is stored.
- 🌍 Users can book dermatologist appointments.
- 🧠 Built using Node.js, Express, MongoDB Atlas, and EJS.

---

## 🏗️ Architecture Overview

The application is deployed using the following **three-tier architecture**:

### 1️⃣ **Presentation Layer (Frontend + DNS + SSL)**

- Users access the website via a custom domain hosted on **Amazon Route 53**.
- **AWS Certificate Manager (ACM)** provides an SSL certificate for HTTPS traffic on port 443.
- Traffic is routed through an **Application Load Balancer (ALB)** which ensures encrypted, balanced, and fault-tolerant request delivery.

---

### 2️⃣ **Application Layer (Private EC2 Tier)**

- The backend application is deployed on **EC2 instances** inside **private subnets** for security.
- EC2 hosts the Node.js/Express server, static AI model logic, and EJS views.
- **Auto Scaling Groups** ensure the application scales based on traffic and remains highly available across multiple **Availability Zones**.
- The **Application Load Balancer** forwards traffic to these instances using Target Groups.

---

### 3️⃣ **Database Layer (MongoDB Atlas)**

- **MongoDB Atlas** is used as the managed NoSQL database solution.
- It securely stores user and appointment data while being accessible only from the application layer.
- Connection credentials are managed through secure environment variables and never exposed publicly.

---

## 🔐 Network & Security Design

- A custom **Virtual Private Cloud (VPC)** is used with isolated **public and private subnets** across two Availability Zones to ensure high availability.
- **Public Subnets** host the Load Balancer and NAT Gateway.
- **Private Subnets** host the EC2 instances.
- **Internet Gateway** allows inbound access to the Load Balancer.
- **NAT Gateway** allows private EC2 instances to access the internet for updates without being directly accessible from outside.
- All security groups and network ACLs are tightly configured for least-privilege access.

---

## 📈 Key Benefits of This Architecture

| Feature                     | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| 🔐 **Security**             | EC2 & DB remain private, accessed only through controlled layers            |
| 🧩 **Scalability**          | Load Balancer & Auto Scaling ensure app handles growing user base           |
| 💡 **Modularity**           | Clear separation of concerns between frontend, backend, and data layers     |
| 🛠️ **Maintainability**     | Easy to debug, extend, and manage across isolated tiers                     |
| ☁️ **Managed Services**     | Reduced overhead using Route 53, ACM, and MongoDB Atlas                     |
| 🌍 **High Availability**    | Deployed across multiple AZs for fault tolerance                            |

---

## 🚀 Deployment Flow (High-Level)

1. Users access the custom domain via HTTPS.
2. Requests reach Amazon Route 53 and are routed to the Load Balancer.
3. Load Balancer decrypts SSL and forwards traffic to EC2 instances.
4. EC2 instances in private subnets handle application logic and AI analysis.
5. EC2 communicates securely with MongoDB Atlas to read/write user data.
6. All outbound traffic from EC2 (e.g., updates) goes via NAT Gateway.
7. The app scales automatically and stays available even during failures.

---

## 📌 Conclusion

This deployment ensures that **Lovely Skins** runs efficiently, securely, and is prepared for real-world user traffic. By leveraging a layered cloud-native architecture, the platform balances security, performance, and scalability—perfectly suited for modern AI-powered web applications.

---


