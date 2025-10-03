# Lab3

### Youtube link:
https://youtu.be/xAhdTvFAcQw <br>

### Reflection Questions

1. What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?<br>
One challenge was understanding that frontend apps like Vue.js cannot read environment variables at runtime. Instead, the values must be baked in during the build stage through GitHub Actions. Figuring out where and how to correctly declare these variables in the workflow file, and making sure the API URLs matched the deployed services, required careful attention.<br> 

2. How does deploying microservices on Azure Web App Service differ from running them locally?<br>
Running locally is straightforward since services can use .env files and communicate directly on localhost. On Azure Web App Service, deployment requires proper configuration of environment variables, networking, and service URLs. The main difference is that Azure handles infrastructure, scaling, and hosting, but you must adapt your code and configuration to work in a managed cloud environment.<br>

3. Why is it important to use environment variables for configurations in a cloud environment?<br>
Environment variables keep sensitive data (like connection strings and API URLs) out of the source code, making the application more secure, portable, and cloud-ready. They allow services to adapt easily to different environments (development, testing, production) without code changes, which aligns with the 12-Factor App principles.<br>



### Repositories links:
https://github.com/sain02/order-service-demo <br>
https://github.com/sain02/product-service-demo-py <br>
https://github.com/sain02/store-front-demo

---
---
## THANKS
