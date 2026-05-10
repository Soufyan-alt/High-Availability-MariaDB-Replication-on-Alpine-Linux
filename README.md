# 🏗️ Enterprise MariaDB High-Availability Cluster

![Status](https://img.shields.io/badge/Status-Production_Ready-success?style=for-the-badge)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Alpine Linux](https://img.shields.io/badge/Alpine_Linux-0D597F?style=for-the-badge&logo=alpine-linux&logoColor=white)

This project demonstrates a robust **Master-Slave Replication** architecture using **MariaDB** deployed on **Alpine Linux** containers. It is designed to provide high data availability, redundancy, and seamless synchronization across isolated network nodes.

---

## 🏛️ System Architecture

The infrastructure is built on a custom Docker bridge network to simulate a real-world data center environment:

1. **Primary Node (`db-master`)**:
   - **IP**: `172.20.0.10`
   - **Function**: Handles all write operations and generates binary logs.
   - **Configuration**: Advanced `log-bin` synchronization enabled.

2. **Replica Node (`db-slave`)**:
   - **IP**: `172.20.0.11`
   - **Function**: Real-time data mirroring for read scaling and failover.
   - **Status**: Continuous IO/SQL thread monitoring.

---

## 🛠️ Key Technical Implementations

* **Optimized Containerization**: Leveraging **Alpine Linux** for a minimal footprint and maximum performance.
* **Network Integrity**: Configured secure `bind-address` protocols to allow inter-container communication while maintaining isolation.
* **Dynamic Replication Flow**: Implementation of a dedicated `replica_user` with granular global privileges.
* **Process Management**: Custom handling of MariaDB daemons and socket paths to ensure system stability.

---

## 🚦 Verification & Health Check

To verify the synchronization, execute the following on the replica node:
```sql
SHOW SLAVE STATUS\G
