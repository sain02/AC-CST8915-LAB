# LAB-8

### Name- Saizal Saini <br> Student Number- 041168394
---
## Deploying and Managing the Algonquin Pet Store (On Steroids)

### YouTube Video Link

https://youtu.be/HKtz-bljPo4

---
# Written Explanation – Task 2: Improving and Extending the Deployment

## Overview
Task 2 focuses on improving the reliability, durability, and scalability of the current Kubernetes deployment that runs MongoDB and RabbitMQ inside the cluster. The existing setup uses simple Deployments with no persistent storage, meaning that all data is lost whenever pods restart or the cluster reboots. To solve these issues, the deployment must be enhanced using StatefulSets, persistent volumes, and replication strategies. Additionally, Azure-managed cloud services are evaluated as potential replacements for self-hosted MongoDB and RabbitMQ.

---

## 1. Improving MongoDB Availability and Persistence

### 1.1 Why Use PersistentVolumeClaim (PVC)?
A PersistentVolumeClaim (PVC) is a Kubernetes resource that requests persistent storage from the cluster.  
With a PVC:
- MongoDB data remains intact even after pod deletion.
- Restarts no longer cause data loss.
- Each replica gets its own dedicated storage.

This is important for database reliability.

### 1.2 Why Use a MongoDB Replica Set?
A MongoDB Replica Set is a group of MongoDB nodes that store the same data.  
It provides:
- High availability  
- Automatic failover  
- Improved data durability  
- Better fault tolerance  

To implement a replica set in Kubernetes, MongoDB must run as a StatefulSet.

### 1.3 Changes Made to MongoDB Deployment
The following enhancements were implemented:
- Converted Deployment → StatefulSet  
- Increased replicas to **3** to support a replica set  
- Added `volumeClaimTemplates` so each pod gets its own PVC  
- Configured a **headless service** (`clusterIP: None`) to provide stable DNS names  
- Mounted persistent storage at `/data/db`  

These changes allow MongoDB to survive restarts, reschedule safely, and run in a highly available configuration.

---

## 2. Adding Persistence to RabbitMQ

### 2.1 Why Persistence Is Required
RabbitMQ stores all its message queues and data inside `/var/lib/rabbitmq`.  
Without persistent storage:
- Messages disappear on pod restart  
- Queue durability cannot be guaranteed  
- RabbitMQ becomes unsafe for production  

### 2.2 Changes Made to RabbitMQ Deployment
To solve this:
- The RabbitMQ Deployment was converted into a StatefulSet  
- `volumeClaimTemplates` were added to create per-pod PVCs  
- Storage was mounted at `/var/lib/rabbitmq`  
- The existing ConfigMap (plugins, definitions) remains mounted  

This ensures that message queues and metadata persist across pod restarts.

---

## 3. Azure Managed Services as Alternatives

### 3.1 Azure Cosmos DB (MongoDB API)
**Purpose:** A fully managed NoSQL database that behaves like MongoDB.  
**Why it's suitable:**
- Automatic backups  
- Global replication  
- High availability  
- No server maintenance required  
- Eliminates the need for replica set configuration and PVCs  

Cosmos DB simplifies operations while providing strong SLAs.

### 3.2 Azure Service Bus
**Purpose:** A fully managed enterprise message broker with queues and topics.  
**Why it's suitable:**
- Built-in durability  
- Guaranteed delivery  
- Auto-scaling  
- Dead-letter queues  
- Zero management overhead  

Service Bus eliminates the need to manage RabbitMQ storage and clustering.

### 3.3 Azure Event Hubs (Optional)
**Purpose:** A cloud-scale event streaming service similar to Kafka.  
**Why it's suitable:**
- High-throughput event ingestion  
- Designed for analytics and large data pipelines  

This is useful when RabbitMQ is used for heavy pub/sub or streaming.

---

## 4. Summary of Improvements

| Component | Previous State | Updated State | Benefit |
|----------|----------------|---------------|---------|
| MongoDB | Deployment, no storage | 3-node StatefulSet + PVC + Replica Set | High availability + persistent storage |
| RabbitMQ | Deployment, ephemeral | StatefulSet + PVC | Durable message queues |
| MongoDB Service | Normal Service | Headless Service | Stable DNS for replica sets |
| Architecture | Self-hosted | Optional Azure Cosmos DB / Service Bus | Managed scaling + reliability |

---

## Conclusion
By converting MongoDB and RabbitMQ into StatefulSets and attaching PersistentVolumeClaims, the deployment becomes significantly more robust. MongoDB gains replication and fault tolerance through a replica set, while RabbitMQ gains durable messaging by storing data persistently.  
Furthermore, Azure-managed alternatives Cosmos DB and Service Bus offer production-grade reliability, automatic scaling, backups, and simplified maintenance, making them strong options for replacing self-hosted services in real-world environments.

---
---
### updated aps-all-in-one.yaml


[text](../aps-all-in-one_.txt)
---

## THANKS