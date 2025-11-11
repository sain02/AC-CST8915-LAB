# LAB-7

### Name- Saizal Saini <br> Student Number- 041168394
---
## CST8915 Full-stack Cloud-native Development: Introduction to Kubernetes Basics

### Youtube Video Link
https://youtu.be/PbaF061BKSE

---

# Algonquin Pet Store – RabbitMQ Configuration Problem Analysis

## Is RabbitMQ a Stateless or Stateful Application?

RabbitMQ is a **stateful application**.  
It maintains critical internal data such as:
- Message queues  
- Routing metadata  
- User credentials and configuration  
- Delivery acknowledgments  

Because RabbitMQ stores these elements, it **depends on persistent data storage**.  
Unlike stateless applications (like frontend web servers) that can restart without losing information, RabbitMQ must **preserve state between restarts** to ensure reliable message delivery and system consistency.

---

## Implications of Running RabbitMQ Without Persistent Storage

In the provided YAML configuration, RabbitMQ is deployed as a **Kubernetes Deployment** without any **PersistentVolumeClaim (PVC)** or **volume mount**.  
This means RabbitMQ data is stored in **ephemeral container storage**, which is lost when the pod is deleted or restarted.

### The consequences include:
- **Message Loss:** All unprocessed messages are erased when the pod restarts.  
- **Queue Loss:** RabbitMQ queues and exchanges are recreated empty upon redeployment.  
- **System Instability:** Services like the `order-service` depending on RabbitMQ for communication may fail or lose data.  
- **Data Volatility:** RabbitMQ cannot guarantee message durability, which defeats its purpose as a reliable message broker.

Essentially, without persistent storage, RabbitMQ behaves as a **stateless message broker**, leading to total data loss during any restart or node rescheduling.

---

## What Happens When the RabbitMQ Pod Is Deleted or Restarted

When the RabbitMQ pod is **deleted or restarted**, the following occurs:
1. The **container and its local filesystem** are destroyed.  
2. Since there’s no persistent volume, RabbitMQ’s **data directory (`/var/lib/rabbitmq`)** is erased.  
3. A **new RabbitMQ instance** starts fresh with no queues, exchanges, or user data.  
4. All **in-transit and unacknowledged messages** are permanently lost.  
5. Other microservices (e.g., `order-service`, `product-service`) will temporarily fail to connect or experience message delivery errors.

### In summary:
> Restarting or deleting the RabbitMQ pod without persistent storage results in complete data loss and breaks reliable messaging between services.

---

## Potential Solutions (Research-Based)

To correctly configure RabbitMQ in Kubernetes and ensure reliability, the following solutions are recommended:

### a. Use a StatefulSet Instead of a Deployment
RabbitMQ should be managed as a **StatefulSet** rather than a Deployment.  
- StatefulSets maintain a **stable network identity** and **dedicated storage per replica**.  
- This ensures that RabbitMQ retains its data and hostname after restarts or scaling operations.

### Comparison: RabbitMQ vs. Azure Service Bus

| **Feature** | **RabbitMQ** | **Azure Service Bus** |
|--------------|---------------|------------------------|
| **Type** | Open-source message broker (self-managed) | Fully managed enterprise-grade messaging service |
| **Hosting** | Runs inside Kubernetes (requires manual setup and maintenance) | Managed by Microsoft Azure with automatic scaling and maintenance |
| **State Management** | Requires persistent volume configuration for data durability | Built-in message persistence handled automatically |
| **Scalability** | Needs manual configuration for clustering and scaling | Auto-scales based on workload, no manual setup required |
| **Reliability** | If pods are deleted or restarted without persistent storage, messages are lost | High reliability with built-in redundancy and fault tolerance |
| **Maintenance** | Developer responsible for managing updates, scaling, and recovery | Managed service — Azure handles updates, patches, and uptime |
| **Use Case Suitability** | Good for lightweight, local, or on-premise microservices | Ideal for cloud-based, enterprise, and production-grade systems |
| **Verdict** | Requires careful configuration and persistent storage to ensure reliability | Solves RabbitMQ configuration issues by providing managed durability and scalability |

**Conclusion:**  
Using **Azure Service Bus** effectively solves the RabbitMQ configuration issues encountered in this lab. It eliminates the need for manual persistence, ensures message durability, and simplifies scaling and maintenance, making it a better fit for cloud-native deployments.

---
## THANKS