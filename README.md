# AetherMart Unified Data & AI Platform 🛒🚀

**A Scalable, Hybrid, and AI Powered Infrastructure for Modern E-Commerce.**
<p align="center"> <img src="https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python" /> <img src="https://img.shields.io/badge/MariaDB-Galera%20Cluster-003545?style=for-the-badge&logo=mariadb" /> <img src="https://img.shields.io/badge/MongoDB-v7.0-47A248?style=for-the-badge&logo=mongodb" /> <img src="https://img.shields.io/badge/AWS-EC2-FF9900?style=for-the-badge&logo=amazonaws" /> <img src="https://img.shields.io/badge/VectorDB-Semantic%20Search-8000FF?style=for-the-badge&logo=apachesolr" /> <img src="https://img.shields.io/badge/LLM%20Embeddings-Transformers-FF6F00?style=for-the-badge&logo=huggingface" /> </p>

## 📖 Project Overview

**AetherMart** has evolved from a niche garage startup selling custom gaming PCs to a leading e-commerce platform for cutting-edge technology and smart home devices. 

AetherMart is an end-to-end hybrid data + AI platform that combines relational storage, NoSQL document models, vector search, semantic retrieval, and real-time synchronization to power intelligent e-commerce experiences.

Originally built as a scalable backend system, AetherMart evolved into an AI-ready platform, capable of supporting semantic product search, embeddings, and agent-like memory retrieval — the same foundational components used in modern LLM-based agent systems.

This project details the engineering of AetherMart's backend data infrastructure. Over the course of six milestones, we transformed a basic relational database into a sophisticated **Hybrid Data Platform** capable of handling high-volume transactions, providing real-time analytics, and supporting AI-driven features.

---

## ⭐ Key Capabilities

### 🤖 AI & Intelligent Retrieval
- Vector Database (FAISS-style architecture)
- Semantic Search using Transformer embeddings
- Natural-language query support (“quiet mechanical keyboard under $100”)
- Embedding pipeline for product descriptions, reviews, and metadata

### 🧠 Agentic AI Foundations
- Vector memory layer for persistent context
- Hybrid structured + unstructured knowledge base
- Real-time world-state sync for agent reliability
- Gemini API integration through Python orchestrators

### 🗄️ Data & Storage
- MariaDB (Galera Cluster for HA + replication scaling)
- MongoDB (Document-oriented for flexible storage)
- Hybrid OLTP + NoSQL ecosystem
- AWS Ubuntu EC2 Instance

### ⚙️ Real-Time Orchestration
- Python ETL pipelines (`pymysql`, `pymongo`)
- Change Data Capture (CDC) triggers + sync queues
- Continuous sync worker (MariaDB → MongoDB)

### 🔐 Governance & Security
- RBAC with granular permission levels
- PII Masking via secure SQL views
- Data lineage + data quality logging
- Environment-variable-based credential isolation
- AWS security Groups 

---

## 🛠️ Tech Stack

### **AI Layer**
- Transformer Embeddings (Gemini / Sentence Transformers)
- Vector Search (FAISS-style VectorDB)
- Semantic Search Pipeline

### **Databases**
- **MariaDB**
  - Galera Cluster (Multi-master HA)
  - Primary–Replica Replication
- **MongoDB**
  - NoSQL Document Store
  - Nested Data Models (profiles, reviews)

### **Python Orchestration**
- `pymysql` – Relational DB automation
- `pymongo` – MongoDB connectivity
- `orchestrator.py` – Full environment automation
- `mongo_sync_worker.py` – Real-time CDC sync

### **Infrastructure**
- AWS EC2 (Ubuntu Linux)
- Security Groups (port-level restrictions)
- Environment Variables for credentials

### **Governance**
- RBAC roles (`alex`, `sarah`, `maria`)
- PII-masked customer views
- Data lineage tracking tables
- Sync audit logs

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

### 🔹 Milestone 4: Schema Evolution & AI Integration
**Goal:** Adapt the schema for new business verticals and prepare for AI integration.
* Updated schema to support "Services" (Consultations) alongside physical products.
* Optimized indexing for complex queries.
* Laid the groundwork for vector embeddings by identifying descriptive fields for Semantic Search and implemented through Gemini API.
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
    ├── Technical_M4.pdf   # Vector Serach, Gemini API, ETL Pipeline
    └── Technical_M5.pdf   # MariaDB to MongoDB
└── Test Scripts/

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

  * **Yash Chetan Doshi**
  * **Dr. David Gomillion** - Part of ISTM 622 Advanced Data Management Coursework

