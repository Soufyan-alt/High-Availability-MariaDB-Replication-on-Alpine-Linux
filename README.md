# 🏗️ High-Availability MariaDB Replication on Alpine Linux

![DevOps](https://img.shields.io/badge/DevOps-Database-blue?style=for-the-badge&logo=devops)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Alpine_Linux-0D597F?style=for-the-badge&logo=alpine-linux&logoColor=white)

This repository demonstrates a professional **Master-Slave Replication** setup using **MariaDB** hosted on lightweight **Alpine Linux** containers. The project focuses on ensuring data consistency and high availability in resource-constrained environments (32-bit architecture).

---

## 🛠️ Tech Stack & Tools

### 🐧 Operating Systems
* ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) **Alpine Linux** (Primary OS for Master & Slave)

### 🐳 Virtualization & Containers
* ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) **Docker Engine** (Containerization)
* ![Network](https://img.shields.io/badge/Network-Isolated_Bridge-green?style=flat-square) **Custom Bridge Network** (172.20.0.0/16)

### 🗄️ Database Management
* ![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white) **MariaDB 11.4** (Binary Logging & Replication)

---

## 🏗️ System Architecture

The environment consists of two distinct Alpine Linux nodes communicating over an isolated virtual network:

1. **Master Node (`db-master`)**:
   - **IP**: `172.20.0.10`
   - **Role**: Primary database for Write/Read operations.
   - **Config**: Binary Logging enabled (`mysql-bin`).

2. **Slave Node (`db-slave`)**:
   - **IP**: `172.20.0.11`
   - **Role**: Read-only replica for backup and redundancy.
   - **Status**: Synchronized with Master via IO/SQL threads.

---

## 🚀 Key Implementation Challenges

During the setup on **32-bit hardware**, several technical hurdles were successfully overcome:

* **Socket Binding**: Resolved `ERROR 2002` by managing manual socket cleanup in `/run/mysqld/`.
* **Network Visibility**: Configured `bind-address=0.0.0.0` to bypass default localhost restrictions.
* **Permission Management**: Fixed directory ownership for `/var/lib/mysql` to allow MariaDB initialization.

---

## 🚦 Status Verification

The replication is confirmed active with the following indicators:
- **`Slave_IO_Running: Yes`**
- **`Slave_SQL_Running: Yes`**

```sql
-- Check Status Command
SHOW SLAVE STATUS\G
