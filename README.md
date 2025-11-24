# AetherMart Unified Data Platform 🛒🚀

**A Scalable, Hybrid, and Intelligent Data Infrastructure for Modern E-Commerce.**

---

## 📖 Project Overview

**AetherMart** has evolved from a niche garage startup selling custom gaming PCs to a leading e-commerce platform for cutting-edge technology and smart home devices. 

This project details the engineering of AetherMart's backend data infrastructure. Over the course of six milestones, we transformed a basic relational database into a sophisticated **Hybrid Data Platform** capable of handling high-volume transactions, providing real-time analytics, and supporting AI-driven features like semantic search.

### 🛠️ Tech Stack
* **Operational Database:** MariaDB (Galera Cluster & Standard Replication)
* **Analytical/Hybrid Database:** MongoDB (NoSQL Document Store)
* **Orchestration & ETL:** Python 3 (`pymysql`, `pymongo`)
* **Infrastructure:** AWS EC2 (Ubuntu Linux), AWS Security Groups
* **Governance:** Custom SQL Auditing, PII Masking, Lineage Tracking

---

## 🏗️ Architecture Evolution (Milestones 1-6)

### 🔹 Milestone 1: The Foundation (Schema Design)
**Goal:** Establish a robust relational schema in 3rd Normal Form (3NF).
* Designed the core Entity Relationship Diagram (ERD).
* Implemented tables for `Customers`, `Products`, `Orders`, `Order_Items`, and `Categories`.
* Enforced data integrity using Primary Keys (PK), Foreign Keys (FK), and constraints.
* **Key Deliverable:** `milestone1.sql` (Core Schema).

### 🔹 Milestone 2: Programmability & Automation
**Goal:** Embed business logic directly into the database for performance and consistency.
* **Stored Procedures:** Created procedures for complex workflows (e.g., `sp_PlaceOrder` to handle transaction atomicity).
* **Triggers:** Implemented automation (e.g., auto-decrementing stock levels after an order).
* **Views:** Created virtual tables for reporting (e.g., `v_QuarterlySales`).
* **Key Deliverable:** `milestone2.sql` (Business Logic Layer).

### 🔹 Milestone 3: High Availability & Scalability
**Goal:** Eliminate single points of failure and ensure zero downtime.
* **Standard Replication:** Configured a Primary-Replica architecture for read-heavy scaling.
    * *Config:* `server_id`, `log_bin`, `read_only=1` on replicas.
* **Galera Cluster:** Implemented a multi-master synchronous cluster for high availability.
    * *Config:* `wsrep_on=ON`, `binlog_format=row`, `wsrep_cluster_address`.
* **Network Security:** Configured AWS Security Groups to allow internal communication on ports `3306`, `4567`, `4568`, `4444` strictly between nodes.
* **Key Deliverable:** `Technical README (Milestone 3).pdf`.

### 🔹 Milestone 4: Schema Evolution & AI Readiness
**Goal:** Adapt the schema for new business verticals and prepare for AI integration.
* Updated schema to support "Services" (Consultations) alongside physical products.
* Optimized indexing for complex queries.
* Laid the groundwork for vector embeddings by identifying descriptive fields for Semantic Search.
* **Key Deliverable:** `milestone4.sql`.

### 🔹 Milestone 5: NoSQL Integration
**Goal:** Introduce flexibility for unstructured data (Reviews & Profiles).
* Provisioned MongoDB v7.0 on AWS EC2.
* Designed NoSQL document schemas for `customer_profiles` (nested addresses) and `reviews` (media arrays).
* Established basic Python connectivity using `pymongo`.

### 🔹 Milestone 6: Operational Mastery (Real-time Hybrid Sync)
**Goal:** Create a unified, real-time ecosystem with end-to-end governance.
* **Real-time Synchronization:**
    * Implemented **Change Data Capture (CDC)** using MariaDB triggers (`sync.sql`).
    * Created persistent **Sync Queues** (`customer_sync_queue`, etc.) in MariaDB.
    * Developed a **Python Sync Worker** (`mongo_sync_worker.py`) to poll queues and update MongoDB in real-time.
* **Advanced Orchestration:**
    * Built `orchestrator.py` to automate the entire lifecycle: Environment Teardown -> Schema Apply -> Data Gen -> Security Apply -> Initial Migration.
* **Data Governance & Security:**
    * **RBAC:** Defined granular roles (`alex`, `sarah`, `maria`).
    * **PII Masking:** Created `v_customers_masked` to hide sensitive data from analysts.
    * **Lineage & Quality:** Implemented `data_lineage_tracker` and `data_quality_logs` tables.
    * **Credential Security:** Migrated all scripts to use Environment Variables.

---

## 🚀 How to Run the Project (Final Version)

The entire platform can be spun up using the Master Orchestrator.

### Prerequisites
1.  **MariaDB** and **MongoDB** installed and running.
2.  **Python 3.x** installed with dependencies:
    ```bash
    pip install pymysql pymongo
    ```
3.  **Environment Variables** set (recommended) or updated in `orchestrator.py`:
    ```bash
    export MARIA_DB_PASS="your_pass"
    export MONGO_ADMIN_PASS="your_mongo_pass"
    ```

### Execution Steps
1.  **Run the Orchestrator:**
    This script wipes the DBs, applies all SQL schemas (M1-M6), sets up security, generates data, and performs the initial migration.
    ```bash
    python3 orchestrator.py
    ```

2.  **Start Real-time Sync:**
    Open a new terminal to keep the sync worker running.
    ```bash
    python3 mongo_sync_worker.py
    ```

3.  **Verify:**
    Make changes in MariaDB (e.g., `UPDATE Customers...`) and observe them reflect instantly in MongoDB.

---

## 📂 Project Structure

```text
├── orchestrator.py        # MASTER SCRIPT: Sets up the entire environment
├── generator.py           # Generates dummy data for MariaDB
├── migrate2.py            # Performs initial bulk load from MariaDB -> MongoDB
├── mongo_sync_worker.py   # REAL-TIME WORKER: Polls queues and syncs data
│
├── SQL_Scripts/
│   ├── milestone1.sql     # Core Schema
│   ├── milestone2.sql     # Stored Procedures & Views
│   ├── milestone4.sql     # Schema Evolution
│   ├── security.sql       # RBAC, PII Views, Governance Tables
│   └── sync.sql           # Sync Triggers & Queue Definitions
│
└── Docs/
    ├── Project.docx       # Original Project Scope
    └── Technical_M3.pdf   # Clustering Documentation
```

-----

## 📽️ Project Artifacts (Presentations & Demos)

Below are the deliverables for each phase of the AetherMart project.

| Milestone | Focus Area | Presentation (PPT) | Demo Video |
| :--- | :--- | :---: | :---: |
| **Milestone 1** | Schema Design & Normalization | [View PPT](https://www.canva.com/design/DAGyWsZ585E/whlZ2AX8RJ17nxbRji5okQ/edit?utm_content=DAGyWsZ585E&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | [Watch Video](https://youtu.be/6DpNZnWCkcw?si=7f5RtIcxqBt0COU3) |
| **Milestone 2** | Advanced SQL & Automation | [View PPT](https://www.canva.com/design/DAGzpjAPUI8/47PSApNyMT-DjHNWPjtoHg/edit?utm_content=DAGzpjAPUI8&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | [Watch Video](https://youtu.be/uDWY3ZVCoJA?si=YSRfshF8Wo-SDdSx) |
| **Milestone 3** | High Availability (Galera/Replication) | [View PPT](https://www.canva.com/design/DAG1mPf_UPw/PsnLuH1gXxfQE1RmWtWaxw/edit?utm_content=DAG1mPf_UPw&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | [Watch Video](https://youtu.be/ZB0uC6ltNyM?si=SZeoa9TeTaIkDOhc) |
| **Milestone 4** | Schema Evolution & Optimization | [View PPT](https://www.canva.com/design/DAG28HQfYWM/Wno6TSmUc4c25-rtu_y9ZA/edit?utm_content=DAG28HQfYWM&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | [Watch Video](https://youtu.be/5xQbXrUCc_o?si=JCL2vGqnyHp0Jxho) |
| **Milestone 5** | NoSQL Introduction | [View PPT](https://www.canva.com/design/DAG3-0RK9LI/mrrjg4nbWtFKrTlqer1rAw/edit?utm_content=DAG3-0RK9LI&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | [Watch Video](https://youtu.be/zWDpPyK2zNo?si=Ym7lj-cM9u_0L1sT) |
| **Milestone 6** | **Final Mastery (Hybrid Real-time Sync)** | [View PPT](https://www.canva.com/design/DAG5dyff2SU/e4QIqmJhNUQoOkwVBMOB8Q/edit?utm_content=DAG5dyff2SU&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton) | [Watch Video](https://youtu.be/ZClVdKPQdMc?si=MbzG55UIMVJGGpHV) |

**Playlist**  | [Watch Video](https://youtube.com/playlist?list=PLK_6HE4o8OUpRB_lch_VKO0WwT5BGM3Dp&si=tLlqEpFPanNx9sdk)

-----

### 👨‍💻 Contributors

  * **Yash Chetan Doshi** - Lead Engineer & Architect
  * **Dr. David Gomillion** - Part of ISTM 622 Advanced Data Management Coursework
  * **Google Gemini**

