
We’ll take a **pharma-themed project**, but the structure works for any enterprise application.

---

# 🌟 Project: Pharma Inventory & Batch Traceability System

**Project Overview (What to Say in Interview):**

> The project is a **web-based system for Novartis** that manages pharmaceutical products, tracks drug batches, monitors inventory, handles expiry and recalls, and maintains audit logs for regulatory compliance.
> It supports multiple users like **Admin, Quality Team, Warehouse, and Auditors**, and ensures **expired or recalled medicines are never distributed**.
> The system is built with **React.js (frontend), Spring Boot (backend), SQL database**, and deployed on **AWS**.

---

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/bdaf15c5-c652-4872-97ca-2f34f79c351e" />


# 🔹 Modules & Functions

Here’s how you can explain each module **confidently**:

---

## 1️⃣ User & Role Management

**Function:**

* Controls **user authentication and authorization**.
* Assigns **roles** like Admin, Quality, Warehouse, and Auditor.

**Key Features:**

* User login/logout
* Role-based access control (RBAC)
* Enable/disable users

**Interview Line:**

> “This module ensures only authorized users access sensitive pharma data.”

---

## 2️⃣ Product Master

**Function:**

* Stores **master data for pharmaceutical products**.
* Acts as a **reference for batches and inventory**.

**Key Features:**

* Add/update product details (name, code, dosage, manufacturer)
* Prevent duplicate product codes
* Maintain consistency across modules

**Interview Line:**

> “Product master ensures all batch and inventory data is linked to consistent product information.”

---

## 3️⃣ Batch & Lot Management

**Function:**

* Tracks **every manufactured batch of a drug**.

**Key Features:**

* Create batches with number, manufacture date, expiry date, and quantity
* Approve or quarantine batches
* Attach batch documents (quality certificates, approvals)

**Interview Line:**

> “Batch management provides full traceability of drug production, ensuring compliance and safety.”

---

## 4️⃣ Inventory Management

**Function:**

* Manages **real-time stock levels** at warehouses.

**Key Features:**

* Receive and issue batches
* Update batch-wise stock quantity
* Prevent negative stock or expired batch usage

**Interview Line:**

> “Inventory module tracks stock accurately and ensures only approved batches are available for distribution.”

---

## 5️⃣ Expiry Monitoring & Alerts

**Function:**

* Monitors **batch expiry dates**.

**Key Features:**

* Highlight near-expiry batches
* Automatically block expired batches
* Notify quality and warehouse teams

**Interview Line:**

> “This module prevents expired drugs from being issued and maintains compliance.”

---

## 6️⃣ Recall Management

**Function:**

* Handles **drug recalls** efficiently.

**Key Features:**

* Mark affected batches as recalled
* Block further distribution
* Track recall reason and history

**Interview Line:**

> “Recall management ensures rapid action in case of quality issues.”

---

## 7️⃣ Audit & Compliance

**Function:**

* Maintains **audit trails** for regulatory inspections.

**Key Features:**

* Log user actions (who, what, when)
* Track changes in batches, inventory, and recalls
* Immutable read-only logs for auditors

**Interview Line:**

> “Audit module helps in compliance and regulatory reporting.”

---

## 8️⃣ Reporting & Dashboard

**Function:**

* Provides **insights and summaries** for business and compliance.

**Key Features:**

* Inventory summary by warehouse
* Near-expiry and recalled batches
* Batch movement history
* Filtered dashboards and charts

**Interview Line:**

> “Dashboards give stakeholders real-time visibility of inventory and batch status.”

---

# 🔹 Optional Micro-Frontend Use Case

**Module:** Reporting & Audit
**Reason:**

* Shared by multiple teams, read-only, frequent UI updates
* Developed as a separate micro-frontend and integrated into main container

**Interview Line:**

> “Micro-frontend allowed independent deployment and scaling of reporting without affecting core modules.”

---

# 🔹 Users and Module Mapping

| Module                 | Users / Actors                            |
| ---------------------- | ----------------------------------------- |
| User & Role Management | Admin                                     |
| Product Master         | Admin, Quality                            |
| Batch Management       | Quality, Admin, Warehouse (view)          |
| Inventory              | Warehouse, Supply Chain, Admin            |
| Expiry Monitoring      | Quality, Warehouse                        |
| Recall                 | Quality, Admin                            |
| Audit & Compliance     | Auditor, Admin, Quality                   |
| Reporting & Dashboard  | Admin, Quality, Warehouse, Business Users |

---

# 🔹 How to Explain Flow in Interview

1. Admin creates **product master**.
2. Quality team creates and approves **batches**.
3. Warehouse receives batches in **inventory**.
4. System monitors **expiry** and prevents invalid distribution.
5. In case of **recall**, Quality blocks the batch.
6. **Audit & Reporting** tracks all actions and provides dashboards.

> “The React frontend communicates with Spring Boot REST APIs, which handle business logic, validations, and database updates.”

---

Perfect! I can create a **database schema diagram** for your **Pharma Inventory & Batch Traceability System**. I’ll include all main tables, their columns, and relationships so you can **visualize it for interviews**.

Here’s the **proposed DB schema**:

---

# 💾 Database Schema

### **1. Users & Roles**

**users**

| Column     | Type      | Notes           |
| ---------- | --------- | --------------- |
| id         | bigint PK | Primary key     |
| username   | varchar   | Unique          |
| password   | varchar   |                 |
| email      | varchar   |                 |
| status     | varchar   | Active/Inactive |
| created_at | timestamp |                 |

**roles**

| Column    | Type      | Notes                           |
| --------- | --------- | ------------------------------- |
| id        | bigint PK | Primary key                     |
| role_name | varchar   | e.g., Admin, Quality, Warehouse |

**user_roles**

| Column  | Type      | Notes                |
| ------- | --------- | -------------------- |
| user_id | bigint FK | references users(id) |
| role_id | bigint FK | references roles(id) |

---

### **2. Product Master**

**products**

| Column            | Type      | Notes               |
| ----------------- | --------- | ------------------- |
| id                | bigint PK | Primary key         |
| product_code      | varchar   | Unique              |
| product_name      | varchar   |                     |
| dosage_form       | varchar   | e.g., Tablet, Syrup |
| strength          | varchar   | e.g., 500mg         |
| manufacturer      | varchar   |                     |
| storage_condition | varchar   |                     |

---

### **3. Batch Management**

**batches**

| Column       | Type      | Notes                         |
| ------------ | --------- | ----------------------------- |
| id           | bigint PK | Primary key                   |
| batch_number | varchar   | Unique                        |
| product_id   | bigint FK | references products(id)       |
| mfg_date     | date      | Manufacture date              |
| expiry_date  | date      | Expiry date                   |
| quantity     | int       | Total quantity                |
| status       | varchar   | APPROVED/QUARANTINED/RECALLED |

---

### **4. Inventory**

**inventory**

| Column        | Type      | Notes                     |
| ------------- | --------- | ------------------------- |
| id            | bigint PK |                           |
| batch_id      | bigint FK | references batches(id)    |
| warehouse_id  | bigint FK | references warehouses(id) |
| available_qty | int       |                           |

**inventory_transactions**

| Column   | Type      | Notes                  |
| -------- | --------- | ---------------------- |
| id       | bigint PK |                        |
| batch_id | bigint FK | references batches(id) |
| txn_type | varchar   | IN/OUT                 |
| quantity | int       |                        |
| txn_date | timestamp |                        |

**warehouses**

| Column   | Type      | Notes          |
| -------- | --------- | -------------- |
| id       | bigint PK |                |
| name     | varchar   | Warehouse name |
| location | varchar   |                |

---

### **5. Recall Management**

**recalls**

| Column        | Type      | Notes                  |
| ------------- | --------- | ---------------------- |
| id            | bigint PK |                        |
| batch_id      | bigint FK | references batches(id) |
| recall_reason | varchar   |                        |
| recall_date   | date      |                        |
| status        | varchar   | ACTIVE/RESOLVED        |

---

### **6. Audit & Compliance**

**audit_logs**

| Column    | Type      | Notes                    |
| --------- | --------- | ------------------------ |
| id        | bigint PK |                          |
| entity    | varchar   | e.g., Batches, Inventory |
| action    | varchar   | CREATE/UPDATE/DELETE     |
| old_value | text      |                          |
| new_value | text      |                          |
| user_id   | bigint FK | references users(id)     |
| timestamp | timestamp |                          |

---

### **7. Optional Reporting**

* **Reporting module** queries `inventory`, `batches`, and `recalls` tables
* No separate tables needed; can use views for dashboards.

---

### **Relationships**

* `users` → `roles` (Many-to-Many via `user_roles`)
* `products` → `batches` (One-to-Many)
* `batches` → `inventory` (One-to-Many)
* `batches` → `recalls` (One-to-One / One-to-Many depending on recall)
* `users` → `audit_logs` (One-to-Many)

---

I can **also create a visual diagram** showing **tables and relationships** in a **clear infographic style**, ready for interviews.

Do you want me to do that next?


