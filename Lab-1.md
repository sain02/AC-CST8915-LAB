# AC-CST8915-LAB
# Lab 1 - Running Algonquin Pet Store

#Submitted By- Saizal Saini (041168394)

## 🎥 Demo Video
Watch the demo here: [YouTube Link](https://youtu.be/IMKwZ_U3LUE)  

---

## 📌 Technical Explanations

### 1. Order Service (Node.js)  
The **Order Service** is responsible for managing the lifecycle of customer orders. Whenever a user places an order through the store-front, this service processes the request, validates the order details, and ensures that the information is correctly recorded. It is the core component that enables the transaction flow of the application.  

This service is built using **Node.js**, which is well-suited for handling asynchronous operations and high I/O workloads. The Order Service typically exposes REST API endpoints that the Store Front calls when a customer checks out. It can also publish or consume messages using tools like **RabbitMQ**, allowing it to communicate order events with other backend services efficiently.  

---

### 2. Product Service (Rust)  
The **Product Service** manages the product catalog for the application. Its main responsibility is to store and serve product information, such as product names, prices, and availability. Whenever the Store Front loads the product listing page, it requests this data from the Product Service.  

This service is implemented in **Rust**, a systems programming language known for its speed, reliability, and memory safety. It exposes APIs (often HTTP-based) that allow the Store Front to retrieve product listings dynamically. By providing structured product data, the Product Service ensures that customers always see up-to-date information when browsing or making purchasing decisions.  

---

### 3. Store Front (Vue.js)  
The **Store Front** is the user-facing interface of the system. It enables customers to browse available products, add items to their cart, and place orders. It essentially acts as the bridge between the user and the backend services, making the overall shopping experience smooth and interactive.  

The Store Front is built with **Vue.js**, a modern JavaScript framework for building responsive and reactive web applications. It communicates with the Product Service via API calls to fetch product data, and it interacts with the Order Service to submit customer orders. By integrating these services into a seamless interface, the Store Front ties the entire system together and provides an accessible, browser-based storefront.  

---

## 📝 Notes / Setup Challenges  
- Configuring the Azure VM and ensuring all services were accessible required proper port setup and firewall configuration.  
- Learned how microservices built in different languages (Node.js, Rust, Vue.js) can integrate and communicate with each other.  
- Gained hands-on experience deploying and testing a cloud-based system end-to-end.  

---

# THANKS