# Microservices Task – Docker & Docker Compose

## 1. Project Overview

This project demonstrates how to containerize four Node.js microservices using Docker and orchestrate them using Docker Compose.

The project includes:

1. User Service
2. Product Service
3. Order Service
4. Gateway Service

Each microservice runs inside its own Docker container. Docker Compose manages the services and connects them using a shared bridge network.

### Technologies Used

- Node.js
- Express.js
- Axios
- Docker
- Docker Compose
- Git
- GitHub
- Ubuntu (WSL2)
- Docker Desktop

## 2. Microservices Architecture

The application consists of four microservices:

| Service | Port | Description |
|---|---|---|
| User Service | 3000 | Manages user information |
| Product Service | 3001 | Manages product information |
| Order Service | 3002 | Manages order information |
| Gateway Service | 3003 | Provides a single entry point for accessing the microservices |

The Gateway Service communicates with the other services through the Docker network.

```text
                  Client / Browser
                         |
                         |
                 Gateway Service
                    Port 3003
                         |
          --------------------------------
          |              |               |
     User Service   Product Service   Order Service
       Port 3000       Port 3001        Port 3002
```

## 3. Project Directory Structure

```text
Microservices-Task/
│
├── Microservices/
│   │
│   ├── user-service/
│   │   ├── app.js
│   │   ├── package.json
│   │   └── Dockerfile
│   │
│   ├── product-service/
│   │   ├── app.js
│   │   ├── package.json
│   │   └── Dockerfile
│   │
│   ├── order-service/
│   │   ├── app.js
│   │   ├── package.json
│   │   └── Dockerfile
│   │
│   └── gateway-service/
│       ├── app.js
│       ├── package.json
│       └── Dockerfile
│
├── docker-compose.yml
├── README.md
└── screenshots/
```

## 4. Prerequisites

Before starting the project, install:

- Git
- Docker Desktop
- Docker Compose
- Node.js and npm (for local development)
- Ubuntu WSL2 (if using Windows)

Verify installation:

```bash
git --version
docker --version
docker compose version
node --version
npm --version
```

<img width="1917" height="222" alt="image" src="https://github.com/user-attachments/assets/f6e72693-ebc8-48fd-a2ea-6fe8e5f2b4d0" />

Ensure Docker Desktop is running.

<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/56441249-86e7-4b53-a8e1-8142e05407d6" />

## 5. Step 1 – Fork the GitHub Repository

1. Open the original repository provided by the trainer.
2. Sign in to GitHub.
3. Click the **Fork** button.
4. Select your GitHub account as the repository owner.
5. Click **Create fork**.

Forking creates a copy of the original repository under your GitHub account.

<img width="1917" height="302" alt="image" src="https://github.com/user-attachments/assets/65bea7f2-55a7-41db-9794-45d8c073d863" />

## 6. Step 2 – Clone the Repository

Open the Ubuntu WSL terminal.

Clone the repository:

```bash
git clone https://github.com/amyadjs-tech/Microservices-Task.git
```

Navigate to the project directory:

```bash
cd Microservices-Task
```

<img width="1917" height="1022" alt="1" src="https://github.com/user-attachments/assets/236e5d91-7388-4493-9d89-d9d0baac62d7" />

<img width="1917" height="1020" alt="2" src="https://github.com/user-attachments/assets/06c6d149-4b03-42bc-8be7-20a9d9007c14" />

<img width="1917" height="995" alt="3 1" src="https://github.com/user-attachments/assets/f096807d-246c-4854-8dfc-6d89d0e29d2f" />

Verify the remote repository:

```bash
git remote -v
```

Expected:

```text
origin https://github.com/amyadjs-tech/Microservices-Task.git (fetch)
origin https://github.com/amyadjs-tech/Microservices-Task.git (push)
```

<img width="1917" height="100" alt="image" src="https://github.com/user-attachments/assets/a95a69f2-8f7e-4122-ba19-87326801f224" />

## 7. Step 3 – Create Dockerfiles

Each microservice requires a Dockerfile.

A Dockerfile contains instructions for building a Docker image.

### 7.1 User Service Dockerfile

Location:

`Microservices/user-service/Dockerfile`

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

### 7.2 Product Service Dockerfile

Location:

`Microservices/product-service/Dockerfile`

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3001

CMD ["npm", "start"]
```

### 7.3 Order Service Dockerfile

Location:

`Microservices/order-service/Dockerfile`

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3002

CMD ["npm", "start"]
```

### 7.4 Gateway Service Dockerfile

Location:

`Microservices/gateway-service/Dockerfile`

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3003

CMD ["npm", "start"]
```

### Dockerfile Instructions Explained

| Instruction | Purpose |
|---|---|
| FROM | Uses the Node.js 20 Alpine base image |
| WORKDIR | Sets the working directory inside the container |
| COPY package*.json | Copies dependency configuration files |
| RUN npm install | Installs Node.js dependencies |
| COPY . . | Copies application source code |
| EXPOSE | Documents the application port |
| CMD | Starts the Node.js application |

<img width="1917" height="1021" alt="3" src="https://github.com/user-attachments/assets/bd03bf4a-833d-4b21-b458-1eb557c064ed" />

<img width="1917" height="1026" alt="4" src="https://github.com/user-attachments/assets/8e2f6c94-cfc0-4d2a-83a5-03e02a0f367b" />

<img width="1917" height="1025" alt="5" src="https://github.com/user-attachments/assets/551f726f-08eb-43c5-b7d8-768c6ebb7252" />


## 8. Step 4 – Configure package.json

Each service requires a start script to run the application.

Navigate to the project directory:

```bash
cd ~/Microservices-Task
```

Run:

```bash
for service in user-service product-service order-service gateway-service; do
    cd "Microservices/$service" || exit 1
    npm pkg set scripts.start="node app.js"
    cd ~/Microservices-Task || exit 1
done
```

Verify the package.json files:

```bash
for service in user-service product-service order-service gateway-service; do
    echo "========== $service =========="
    cat "Microservices/$service/package.json"
    echo ""
done
```

Each package.json should contain:

```json
"scripts": {
  "start": "node app.js"
}
```

## 9. Step 5 – Create docker-compose.yml

Create a `docker-compose.yml` file in the project root directory.

```yaml
services:
  user-service:
    build:
      context: ./Microservices/user-service
    ports:
      - "3000:3000"
    networks:
      - microservices-network

  product-service:
    build:
      context: ./Microservices/product-service
    ports:
      - "3001:3001"
    networks:
      - microservices-network

  order-service:
    build:
      context: ./Microservices/order-service
    ports:
      - "3002:3002"
    networks:
      - microservices-network

  gateway-service:
    build:
      context: ./Microservices/gateway-service
    ports:
      - "3003:3003"
    environment:
      USER_SERVICE_URL: http://user-service:3000
      PRODUCT_SERVICE_URL: http://product-service:3001
      ORDER_SERVICE_URL: http://order-service:3002
    depends_on:
      - user-service
      - product-service
      - order-service
    networks:
      - microservices-network

networks:
  microservices-network:
    driver: bridge
```

### Docker Compose Explanation

- `services`: Defines the four microservices.
- `build`: Specifies the Docker build context.
- `ports`: Maps host ports to container ports.
- `environment`: Configures backend service URLs for the Gateway.
- `depends_on`: Starts backend containers before the Gateway.
- `networks`: Connects all services using a shared bridge network.

Note: `depends_on` controls startup order but does not guarantee that an application is ready to accept requests.

<img width="1917" height="62" alt="image" src="https://github.com/user-attachments/assets/ff5f52ce-b7d3-41c3-bb36-f199628e4494" />
<img width="1917" height="145" alt="image" src="https://github.com/user-attachments/assets/31a1d34d-9a2f-40e6-9821-b84e8d230e97" />
<img width="1917" height="1016" alt="image" src="https://github.com/user-attachments/assets/d5254582-c66e-47b2-b019-b4215a28a5ea" />


## 10. Step 6 – Validate Docker Compose

Run:

```bash
cd ~/Microservices-Task
docker compose config
```

This validates the Compose configuration.

## 11. Step 7 – Build and Start the Containers

Run:

```bash
docker compose up --build -d
```

Explanation:

- `up`: Creates and starts containers.
- `--build`: Builds Docker images.
- `-d`: Runs containers in detached mode.

Check running containers:

```bash
docker ps
```

Or:

```bash
docker compose ps
```

Expected services:

```text
microservices-task-user-service-1
microservices-task-product-service-1
microservices-task-order-service-1
microservices-task-gateway-service-1
```

## 12. Step 8 – Test the Microservices

After starting the containers, verify each service.

### User Service

```bash
curl -i http://localhost:3000/users
```

Browser:

http://localhost:3000/users

### Product Service

```bash
curl -i http://localhost:3001/products
```

Browser:

http://localhost:3001/products

### Order Service

```bash
curl -i http://localhost:3002/orders
```

Browser:

http://localhost:3002/orders

### Gateway Service

Test the User endpoint:

```bash
curl -i http://localhost:3003/api/users
```

Test the Product endpoint:

```bash
curl -i http://localhost:3003/api/products
```

Test the Order endpoint:

```bash
curl -i http://localhost:3003/api/orders
```

A successful test should return an HTTP 200 response with the expected JSON data.

## 13. Step 9 – Docker Networking

All four microservices communicate using a shared Docker bridge network.

Network name in Compose:

```text
microservices-network
```

Inside Docker, containers communicate using their service names.

Examples:

```text
http://user-service:3000
http://product-service:3001
http://order-service:3002
```

The Gateway uses these addresses to access the backend services.

View Docker networks:

```bash
docker network ls
```

## 14. Step 10 – Troubleshooting

### Issue 1: Missing npm start script

Error:

```text
npm ERR! Missing script: "start"
```

Solution:

```bash
npm pkg set scripts.start="node app.js"
```

Make sure the command is executed inside the affected service directory.

### Issue 2: Port 3000 Already Allocated

Error:

```text
Bind for 0.0.0.0:3000 failed: port is already allocated
```

Cause:

Another application or container is using port 3000.

In this project, a Grafana container was using port 3000.

Check:

```bash
docker ps
```

Stop Grafana if it is not required:

```bash
docker stop grafana
```

Restart the microservices:

```bash
docker compose up -d
```

### Issue 3: Docker Container Not Starting

Check container logs:

```bash
docker compose logs
```

Check a specific service:

```bash
docker compose logs user-service
```

### Issue 4: Docker Compose YAML Error

Run:

```bash
docker compose config
```

Check YAML indentation, service names, ports, and build context paths.

### Issue 5: GitHub Authentication Failed

Error:

```text
remote: Invalid username or token.
Password authentication is not supported for Git operations.
```

Cause:

GitHub does not support account-password authentication for Git operations over HTTPS.

Solution:

Create a Fine-grained Personal Access Token with:

- Resource owner: Your GitHub account
- Repository access: All repositories, or only the repository being pushed
- Contents permission: Read and write
- Metadata permission: Read-only

Generate the token from:

https://github.com/settings/personal-access-tokens

Push using:

```bash
git -c credential.helper= push origin main
```

Enter the GitHub username and use the token as the password.

Never share the token or commit it to the repository.

## 15. Step 11 – Push the Project to GitHub

Navigate to the project directory:

```bash
cd ~/Microservices-Task
```

Check Git status:

```bash
git status
```

Check the remote repository:

```bash
git remote -v
```

Stage all changes:

```bash
git add .
```

Commit:

```bash
git commit -m "Containerize Node.js microservices using Docker Compose"
```

Push:

```bash
git -c credential.helper= push origin main
```

Verify:

```bash
git status
```

After a successful push, Git should show:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

### GitHub Repository

https://github.com/amyadjs-tech/Microservices-Task

## 16. Step 12 – Screenshots

Capture the following screenshots for assignment documentation.

### Screenshot 1 – Docker Containers Running

Run:

```bash
docker ps
```

Save the screenshot as:

`screenshots/docker-containers.png`

### Screenshot 2 – Docker Compose Status

Run:

```bash
docker compose ps
```

Save as:

`screenshots/docker-compose-status.png`

### Screenshot 3 – API Testing

Run the six curl commands from the testing section.

Save as:

`screenshots/api-testing.png`

### Screenshot 4 – Docker Desktop

Open Docker Desktop and capture all four running microservices.

Save as:

`screenshots/docker-desktop.png`

Once the images are added to the repository, they can be displayed here:

![Docker containers](screenshots/docker-containers.png)

![Docker Compose status](screenshots/docker-compose-status.png)

![API testing](screenshots/api-testing.png)

![Docker Desktop](screenshots/docker-desktop.png)

## 17. Step 13 – Stop and Remove Containers

Stop the services:

```bash
docker compose stop
```

Stop and remove the Compose containers and network:

```bash
docker compose down
```

Rebuild and restart:

```bash
docker compose up --build -d
```

## 18. Step 14 – Prepare ZIP Submission

Create a submission directory containing the required project files.

```bash
cd ~/Microservices-Task

mkdir -p submission

cp -r Microservices/user-service submission/
cp -r Microservices/product-service submission/
cp -r Microservices/order-service submission/
cp -r Microservices/gateway-service submission/

cp docker-compose.yml README.md submission/
```

If screenshots have been captured:

```bash
cp -r screenshots submission/
```

Remove any copied dependency directories:

```bash
find submission -type d -name node_modules -prune -exec rm -rf {} +
```

Because the services are now directly inside `submission/`, change the Docker Compose build contexts in `submission/docker-compose.yml` to:

```yaml
context: ./user-service
context: ./product-service
context: ./order-service
context: ./gateway-service
```

Each context belongs under its corresponding service's `build` section.

Validate the submission:

```bash
cd submission
docker compose config
cd ..
```

Create the ZIP:

```bash
zip -r Microservices-Task.zip submission
```

Verify its contents:

```bash
unzip -l Microservices-Task.zip
```

The ZIP includes the Dockerfiles, application source code, Compose configuration, README, and any screenshots added.

## 19. Conclusion

This project demonstrates:

- Containerization of Node.js applications using Docker
- Dockerfile creation for individual microservices
- Multi-container orchestration using Docker Compose
- Inter-container communication through Docker networking
- Local testing of REST API endpoints
- Troubleshooting Docker and GitHub authentication issues
- Git version control and pushing code to GitHub

The four microservices were successfully built and started using Docker Compose, and the project changes were pushed to GitHub.


**Repository:** [Microservices-Task](https://github.com/amyadjs-tech/Microservices-Task)

