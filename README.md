# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

## Services and Endpoints

### **User Service**
- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**  
    ```
    curl http://localhost:3000/users
    ```
    Or open in your browser: [http://localhost:3000/users](http://localhost:3000/users)

---

<img width="1917" height="312" alt="image" src="https://github.com/user-attachments/assets/75d476c6-390d-46ab-88d5-43150da1b946" />

<img width="1917" height="171" alt="45" src="https://github.com/user-attachments/assets/b5ff50b6-6fff-4071-a197-6af28103f9b6" />

### **Product Service**
- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**  
    ```
    curl http://localhost:3001/products
    ```
    Or open in your browser: [http://localhost:3001/products](http://localhost:3001/products)

---
<img width="1917" height="317" alt="46" src="https://github.com/user-attachments/assets/194a1dc8-9828-455f-8198-4c81e8579d4b" />

<img width="1917" height="137" alt="image" src="https://github.com/user-attachments/assets/a4065d79-0d92-487c-90d8-400e1e53ef8b" />


### **Order Service**
- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**  
    ```
    curl http://localhost:3002/orders
    ```
    Or open in your browser: [http://localhost:3002/orders](http://localhost:3002/orders)

---

<img width="1917" height="290" alt="48" src="https://github.com/user-attachments/assets/06ba27cf-f959-4f2a-b94e-1caf767fe4f3" />

<img width="1917" height="141" alt="image" src="https://github.com/user-attachments/assets/5ded1808-708e-4fce-9bae-cc73f81666c9" />

### **Gateway Service**
- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**  
    ```
    curl http://localhost:3003/api/users
    ```
  - **Products:**  
    ```
    curl http://localhost:3003/api/products
    ```
  - **Orders:**  
    ```
    curl http://localhost:3003/api/orders
    ```

---

<img width="1917" height="912" alt="image" src="https://github.com/user-attachments/assets/11b84dd2-098c-445b-8151-8c3026fa2e75" />


## Instructions
1. Start all services using the `docker-compose` file:
   ```
   docker-compose up
   ```
2. Once the services are running, use the above endpoints to verify the functionality.

Happy testing!
