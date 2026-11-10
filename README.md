2-Tier Microservices Architecture Deployment Using Docker, Nginx & Node.js

!Docker !Nginx !Node.js !Express.js !Architecture !Docker Compose

Project Overview

This project demonstrates the implementation and deployment of a 2-Tier Microservices Architecture using Docker, Nginx Reverse Proxy, and Node.js.

The application consists of independently deployed Node.js microservices, with Nginx serving as a centralized entry point to route incoming HTTP requests to the appropriate backend services using proxy_pass.

Docker is used to containerize individual services, while Docker Compose simplifies multi-container deployment, networking, and service management.

The primary objective is to understand containerized application deployment, reverse proxy configuration, service discovery, and communication between distributed application components.

Architecture Diagram

                    CLIENT / BROWSER
                           |
                           |
                      HTTP :80
                           |
                           v
                +----------------------+
                |                      |
                |       NGINX          |
                |   Reverse Proxy      |
                |   Port: 80           |
                |                      |
                +----------------------+
                           |
                     proxy_pass
                           |
                +----------+----------+
                |                     |
                v                     v
       +----------------+    +------------------+
       |                |    |                  |
       |  USER SERVICE  |    | PRODUCT SERVICE  |
       |                |    |                  |
       |   Node.js      |    |    Node.js       |
       |   Express.js   |    |    Express.js    |
       |   Port: 3001   |    |    Port: 3002    |
       |                |    |                  |
       +----------------+    +------------------+
                |                     |
                +----------+----------+
                           |
                    DOCKER NETWORK
                           |
                  DOCKER COMPOSE

Architecture Workflow
The client sends an HTTP request to the Nginx reverse proxy.
Nginx listens on port 80 and evaluates the incoming request URL.
Based on the URL path, Nginx forwards the request using proxy_pass.
The appropriate Node.js microservice processes the request.
The backend service returns the response to Nginx.
Nginx forwards the response to the client.
Technology Stack
Technology	Purpose
Node.js	Backend application runtime
Express.js	REST API development
Nginx	Reverse proxy and request routing
Docker	Application containerization
Docker Compose	Multi-container orchestration
Docker Network	Inter-container communication
Linux	Deployment environment
Git & GitHub	Version control and project management
Project Structure

2-tier-microservices/
│
├── nginx/
│   └── nginx.conf
│
├── user-service/
│   ├── server.js
│   ├── package.json
│   └── Dockerfile
│
├── product-service/
│   ├── server.js
│   ├── package.json
│   └── Dockerfile
│
├── docker-compose.yml
│
└── README.md

Microservices Description
1. Nginx Reverse Proxy

Nginx acts as the single entry point for incoming application traffic.

Responsibilities:

Accept incoming HTTP requests on port 80.
Route requests based on URL paths.
Forward requests to the appropriate Node.js backend.
Handle communication between clients and backend services.
Provide a centralized entry point for the application.

Routing Configuration

Request Path	Backend Service	Internal Port
/users	User Service	3001
/products	Product Service	3002
2. User Microservice

A standalone Node.js application developed using Express.js.

Responsibilities:

Handle user-related API requests.
Return user information in JSON format.
Process requests routed through Nginx.

API Endpoint

http
GET /users


Sample Response

json
[
  {
    "id": 1,
    "name": "John"
  },
  {
    "id": 2,
    "name": "David"
  }
]

3. Product Microservice

A separate Node.js application responsible for product-related API operations.

Responsibilities:

Handle product-related API requests.
Return product information in JSON format.
Process requests routed through Nginx.

API Endpoint

http
GET /products


Sample Response

json
[
  {
    "id": 101,
    "name": "Laptop"
  },
  {
    "id": 102,
    "name": "Mobile"
  }
]

Prerequisites

Ensure the following tools are installed before deploying the application:

Docker Engine
Docker Compose V2
Git
Linux / Ubuntu or Windows with Docker Desktop

Verify the installations:

bash
docker --version
docker compose version
git --version

Deployment Guide
Step 1: Clone the Repository
bash
git clone https://github.com/YOUR_USERNAME/2-tier-microservices.git

cd 2-tier-microservices

Step 2: Build Docker Images

Build individual microservice images using Docker Compose.

bash
docker compose build

Step 3: Start Application Containers

Deploy all services in detached mode.

bash
docker compose up -d

Step 4: Verify Container Status
bash
docker ps


Expected deployment:

Container	Component	Port
nginx-proxy	Nginx Reverse Proxy	80
user-service	User Microservice	3001 (internal)
product-service	Product Microservice	3002 (internal)
Step 5: Verify Application Logs
bash
docker compose logs -f

Application Testing & Validation

Once all containers are running, verify the application using a browser, Postman, or cURL.

1. Verify Nginx

bash
curl http://localhost/


Expected response:

text
Nginx Reverse Proxy is Running!


2. Test User Microservice

bash
curl http://localhost/users


Expected response:

json
[
  {"id":1,"name":"John"},
  {"id":2,"name":"David"}
]


3. Test Product Microservice

bash
curl http://localhost/products


Expected response:

json
[
  {"id":101,"name":"Laptop"},
  {"id":102,"name":"Mobile"}
]

Docker Management Commands
Command	Description
docker ps	Display running containers
docker images	List available Docker images
docker compose build	Build application images
docker compose up -d	Start all application services
docker compose down	Stop and remove containers
docker compose restart	Restart services
docker compose logs -f	Monitor application logs
docker compose ps	Check service status
docker compose down --rmi local	Remove containers and locally built images
docker exec -it nginx-proxy sh	Access Nginx container shell
Key Implementation Highlights
Microservices Architecture: Independent Node.js services for user and product operations.
Reverse Proxy: Nginx routes HTTP requests using proxy_pass.
Containerization: Each microservice runs inside its own Docker container.
Service Discovery: Docker Compose service names enable internal container communication.
Container Networking: Services communicate through a dedicated Docker network.
Centralized Entry Point: Clients access backend services through Nginx rather than exposing each backend port publicly.
Simplified Deployment: Docker Compose manages the entire application stack.
Security & Production Considerations

The current implementation is designed as a learning and demonstration project. Before production deployment, consider:

Configure HTTPS using SSL/TLS certificates.
Implement Nginx security headers.
Add container health checks.
Run containers using non-root users.
Configure CPU and memory resource limits.
Use environment variables and secrets management.
Implement centralized logging and monitoring.
Configure proper backend readiness and failure handling.
Use pinned and regularly updated container image versions.
Future Enhancements

The architecture can be extended with additional DevOps and cloud-native capabilities:

Integrate MongoDB for persistent data storage.
Implement Nginx load balancing with multiple backend replicas.
Configure HTTPS using Let's Encrypt.
Implement CI/CD pipelines using Jenkins or GitHub Actions.
Deploy the application on AWS EC2.
Integrate Prometheus and Grafana for monitoring.
Implement centralized logging using the ELK Stack.
Introduce Kubernetes for container orchestration.
Learning Outcomes

Through this project, the following practical concepts are demonstrated:

Understanding 2-Tier application architecture.
Developing REST APIs using Node.js and Express.js.
Configuring Nginx as a reverse proxy.
Understanding Nginx proxy_pass directives.
Building and managing Docker images.
Deploying multiple containers using Docker Compose.
Understanding Docker bridge networking and service discovery.
Testing and validating microservice communication.
Troubleshooting containerized applications.
Author

Your Name

DevOps Engineer | Cloud | Docker | Kubernetes | AWS | Linux | Jenkins | CI/CD

GitHub: Your GitHub Profile
LinkedIn: Your LinkedIn Profile
License

This project is available for educational and learning purposes.

Acknowledgements

Built as a hands-on DevOps project to demonstrate containerization, reverse proxy configuration, and multi-service application deployment.

If you find this project useful, please consider giving this repository a ⭐ on GitHub.
