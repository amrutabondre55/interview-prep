
### ✅ **Interview Introduction**

> Hi, my name is **Amruta Bondre**.
> I’m a **Java Full Stack Developer** with **over 3 years of experience** at **Cognizant Technology Solutions**.
> I have hands-on experience building **end-to-end web applications** using **Java, Spring Boot, REST APIs, React.js, AWS services, and CI/CD**.

> In my previous project, I worked on a **Pharma Inventory and batch Traceability System** for **Novartis Pharma**.
> I was involved in **backend API development, frontend UI development, micro-frontend implementation, and cloud deployment**.
> My responsibilities included developing **Spring Boot REST APIs**, building **React components**, writing **unit tests**, and **supporting production issues**.

> I have worked closely in **Agile Scrum teams**, collaborated with **product managers**, and paired with team members.
> Now I'm looking for an opportunity where I can **contribute effectively and continue to grow**.
>
> ---
>
> This is **very good content** 👍
I’ll **polish the language**, fix grammar, and make it **more natural and interview-ready**, while keeping it **simple and crisp** (no over-engineering).

Below is the **refined version you can directly speak**.

---

## ✅ Q1) Explain me your project? (Interview Answer)

> I worked on a **pharma inventory and batch traceability system** for **Novartis**.
> The application is used to manage pharmaceutical products, track drug batches, monitor inventory, handle expiry and recalls, and maintain audit logs for compliance.

> Users such as **Admin, Quality team, Warehouse, and Auditors** use the system.

> The system ensures that **expired or recalled medicines are not distributed**, and all critical actions are recorded for **regulatory audits**.
> It is built using **React for the frontend**, **Spring Boot for the backend**, **SQL for the database**, and deployed on **AWS**.

---

## ✅ Q2) What was your role and responsibilities within the project?

> I worked as a **Java Full Stack Developer**.
> My responsibilities included:

* Developing **Spring Boot REST APIs**
* Building **React UI components**
* Implementing **business validations** for batches and inventory
* Writing **unit tests** using JUnit and Mockito
* Fixing **production issues**
* Working closely with the team in **Agile Scrum**

---

## ✅ Q3) What is the use case implemented for Micro-Frontend?

### (Reporting & Audit Module – Simple Explanation)

### 🔹 Use Case

> We implemented **micro-frontend** for the **Reporting and Audit module**.

> It is a **read-only module**, used by **multiple teams**, and requires **frequent UI changes** like adding new reports, filters, and dashboards.

---

### 🔹 Why This Module Was Chosen

> Reporting and Audit is a **separate and shared application** used across different systems within the organization.
> It is commonly used by **Quality, Warehouse, Admin, and Audit teams**, which made it a good candidate for micro-frontend.

---

### 🔹 How Micro-Frontend Helped

> The Reporting and Audit UI was developed as a **separate application** and integrated into the **main container app**.
> This allowed the team to:

* Deploy reports **independently**
* Add new dashboards **without impacting other modules**
* Scale the reporting UI **separately**

---

### 🔹 Integration with Other Applications

> The Reporting and Audit micro-frontend consumed data from:

* **Quality systems** (batch status and recalls)
* **Warehouse systems** (inventory movements)
* Backend services using **common REST APIs**

> The micro-frontend handled only the **UI layer**, while all **business logic remained in the backend**.

---

## 🎯 One-Line Interview Summary

> We used micro-frontend for the Reporting and Audit module because it is a shared, read-only feature used by multiple teams and required independent UI deployment without impacting core inventory functionality.

---

### 🔥 Final Tip (Important)

If interviewer interrupts, just say:

> “Reporting and Audit was a shared, read-only module with frequent UI changes, so micro-frontend helped us deploy and scale it independently.”

---

https://github.com/amrutabondre55/micro-frontend/blob/main/faq.md

---
---
Below is a **clean, step-by-step interview-ready answer**, including **Docker, ECR, and WAF (IP restriction)**, exactly aligned with what you described.
You can speak this **confidently in interviews**.
---

## 🎯 Final 30-Second Interview Summary

> **“We follow a CI/CD-based deployment. Developers raise PRs, seniors review the code, and once merged into the main branch, GitHub Actions triggers the pipeline. GitHub Actions builds the backend application
A Docker image is created using a Dockerfile, then  Docker image pushed to Amazon ECR, and deployed on ECS Fargate.
> The frontend is built and deployed to S3 and served through CloudFront with cache invalidation. AWS WAF is used to restrict access using allowed IPs. This approach ensures automated, secure, scalable, and reliable deployments.”**

---

## ✅ Step-by-Step Deployment Process (Interview Answer)

### **Step 1: Code Development**

Developers implement user stories on their **local machine** and push the code to their **feature branch or forked repository**.

---

### **Step 2: Pull Request & Code Review**

Developers raise a **Pull Request (PR)** to the **main branch**.
Senior developers review the code for **quality, security, and standards**.

---

### **Step 3: Merge to Main Branch**

Once the PR is approved, it is **merged into the main branch**, which acts as the **deployment trigger**.

---

### **Step 4: CI/CD Pipeline Trigger (GitHub Actions)**

As soon as the code is merged:

* **GitHub Actions pipeline is triggered automatically**
* Separate workflows exist for **backend and frontend**

---

## 🔹 Backend Deployment (ECS Fargate)

### **Step 5: Backend Build & Docker Image Creation**

* GitHub Actions builds the backend application
* A **Docker image** is created using a Dockerfile

---

### **Step 6: Push Docker Image to Amazon ECR**

* The Docker image is tagged with a version
* The image is pushed to **Amazon ECR (Elastic Container Registry)**

---

### **Step 7: Deploy to ECS Fargate**

* ECS pulls the latest Docker image from **ECR**
* ECS **updates the running task definition**
* Application is deployed to **Dev and QA (pre-production)** environments
* ECS Fargate handles **scaling and infrastructure automatically**

---

### **Step 8: Security Using WAF**

* **AWS WAF** is attached to the Application Load Balancer / CloudFront
* Only **allowed IPs** can access backend APIs
* Protects against **unauthorized access and common attacks**

---

### **Step 9: Testing & Production Approval**

* Developers perform testing in Dev/QA
* After validation, **Senior Developer deploys to Production**
* Deployment happens only after **Product Manager approval**

---

## 🔹 Frontend Deployment (S3 + CloudFront)

### **Step 10: Frontend Build Creation**

* GitHub Actions builds the **React application**
* A production-ready **static artifact** is generated

---

### **Step 11: Upload to S3 Bucket**

* Existing build files in the S3 bucket are **deleted**
* New build artifacts are uploaded to **S3**

---

### **Step 12: CloudFront Cache Invalidation**

* After upload, **CloudFront cache is invalidated**
* Ensures users receive the **latest frontend content**

---

### **Step 13: Frontend Security with WAF**

* **AWS WAF** is also applied to CloudFront
* Allows only **whitelisted IPs**
* Protects against **malicious traffic and attacks**

---

## 🎯 Final 30-Second Interview Summary

> **“We follow a CI/CD-based deployment. Developers raise PRs, seniors review the code, and once merged into the main branch, GitHub Actions triggers the pipeline. The backend is containerized using Docker, pushed to Amazon ECR, and deployed on ECS Fargate. The frontend is built and deployed to S3 and served through CloudFront with cache invalidation. AWS WAF is used to restrict access using allowed IPs. This approach ensures automated, secure, scalable, and reliable deployments.”**

---
