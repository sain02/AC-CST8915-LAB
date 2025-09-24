# Lab 2 - Configurations & Backing Services  

#Submitted By - Saizal Saini (041168394)  

## 🎥 Demo Video  
Watch the demo here: [YouTube Link](https://youtu.be/OK6vO1at3P4)  

---

## 📌 What the Demo Includes  
- Store-front running in the browser, hosted on its own Azure VM.  
- Public IPs of the four VMs (**store-front, order-service, product-service, RabbitMQ**) shown in the Azure portal/terminal.  
- Proof that **order-service** and **product-service** are using environment variables (e.g., `.env` files or logs).  
- Store-front loading products from the **product-service** VM.  
- An order placed through the **order-service** VM.  
- The order-service successfully sending a message to **RabbitMQ** on its dedicated VM, shown via the RabbitMQ Management UI.  

---

---

## 📝 Reflection Questions  

**1. What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?**  
I updated both services to load configuration values like database URLs and ports from environment variables instead of hardcoding them. This makes the services portable, easier to configure in different environments, and allows smooth integration with external backing services.  

**2. Why is it important to use environment variables instead of hard-coding configurations in your application?**  
Using environment variables keeps sensitive information like passwords and API keys out of the code. It also allows configuration to change per environment (development, testing, production) without changing the application’s source code.  

**3. Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?**  
Separate repositories keep microservices independent, so they can be built, tested, and deployed individually. This improves scalability, reduces conflicts between services, and allows teams to update or scale each service without affecting the others.  

---

## ⚡ Notes / Setup Challenges  
- Learned how to configure services to use `.env` files for sensitive values.  
- Faced challenges setting up environment variables correctly across multiple VMs.  
- Gained experience working with **RabbitMQ** as a dedicated backing service.  
- Saw how separating services into different repos makes the system easier to manage and scale.  

---

# THANKS  
