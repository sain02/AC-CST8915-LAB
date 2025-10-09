# LAB-4

### Name- Saizal Saini <br> Student Number- 041168394
---
## Full-stack Cloud-native Development: Introduction to Docker

### YouTube Video Link:
https://youtu.be/cp-LjFAMrDI 

### Reflection Questions:

**1. What are the main differences between a Docker image and a Docker container?**  
A Docker image is a read-only template containing the application code, dependencies, and configuration needed to run a program. A Docker container is a running instance of an image that includes a writable layer, making it an executable and isolated environment for the application.

**2. Explain how Docker's layered architecture improves efficiency.**  
Docker's layered architecture allows images to be built in layers, with each layer representing a set of changes. This enables reuse of common layers across multiple images, reduces storage usage, and speeds up builds by only updating changed layers instead of the whole image.

**3. Why does each container get its own writable layer?**  
Each container has its own writable layer to allow changes to the filesystem without affecting the original image or other containers. This ensures isolation, so modifications, temporary files, or logs created by one container do not interfere with others.

**4. What are the benefits of using Docker Compose over running containers individually?**  
Docker Compose simplifies managing multi-container applications by defining all services, networks, and volumes in a single YAML file. It enables easy startup, scaling, and consistent configuration of multiple containers with a single command, reducing complexity and manual setup.

---


---

# THANKS