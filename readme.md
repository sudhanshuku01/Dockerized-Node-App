

# Microservices-Based Node.js App with MongoDB, NGINX, and Docker

Welcome! This project shows how to build and run a Node.js application using **microservices**. Don't worry if you're new to the idea of microservices—I'll walk you through everything. We also use Docker, which helps package everything up neatly so that it's easy to run, no matter where you are.

By the end, you'll see how to split an application into small parts (called **services**) and manage them using Docker and Docker Compose. This will make your application easier to scale and maintain.

## Table of Contents
- [Overview](#overview)
- [What are Microservices?](#what-are-microservices)
- [Technologies Used](#technologies-used)
- [How to Set Up the Project](#how-to-set-up-the-project)
- [Understanding the GitHub Actions Workflow](#understanding-the-github-actions-workflow)
- [Breaking Down the Docker Components](#breaking-down-the-docker-components)
- [Docker Compose: Bringing Everything Together](#docker-compose-bringing-everything-together)
- [Key Concepts Explained](#key-concepts-explained)
  - [Service Isolation](#service-isolation)
  - [Scaling](#scaling)
  - [Reverse Proxy with NGINX](#reverse-proxy-with-nginx)
  - [Environment Variables](#environment-variables)
- [Contributing](#contributing)
- [License](#license)

## Overview

This project is a basic **microservices** setup using Node.js, MongoDB, and NGINX. If these words sound unfamiliar, don't worry—I'll break them down in simple terms. The idea here is to build a **modular** application, where different parts (called services) are independent but work together.

For example:
- **Node.js** is the app where we write the backend code (like handling user requests).
- **MongoDB** is the database that stores your application's data.
- **NGINX** is used to handle incoming traffic and distribute it across the app for better performance.
  
We use **Docker** to package everything into containers, which are like small, isolated environments for each part of our app. **Docker Compose** helps us manage and run these containers together as one system.

---

## What are Microservices?

A **microservice** is just a small, independent piece of an application that does one thing really well. In this project:
- **Node.js** is the service that runs the backend code.
- **MongoDB** is the service that stores data.
- **NGINX** helps direct incoming traffic.

With microservices, each part of the app runs independently, which makes it easier to manage, scale, and update. If one part fails or needs to be updated, the rest of the system can keep running.

### Why Microservices?

1. **Independence**: Each service is its own piece. If one service goes down (e.g., MongoDB), the others can still work.
2. **Scalability**: You can scale each service independently. If your Node.js app needs more processing power, you can run multiple copies without affecting MongoDB or NGINX.
3. **Easy Maintenance**: You can update one service without disrupting the entire app.
4. **Flexibility**: Different services can use different programming languages or databases. In this project, we use Node.js for the app and MongoDB for the database.

---

## Technologies Used

- **Node.js**: JavaScript runtime for building the backend service.
- **MongoDB**: NoSQL database to store and retrieve data.
- **NGINX**: A reverse proxy to distribute and manage traffic.
- **Docker**: To package and run the services in isolated containers.
- **Docker Compose**: To manage and run multiple containers together.
- **GitHub Actions**: To automate building and pushing the Docker image.

---

## How to Set Up the Project

### Prerequisites

Before you start, make sure you have these installed on your computer:
- Docker
- Docker Compose

### Step-by-Step Setup

1. **Clone the repository**:
   Open your terminal and run:
   ```bash
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
   ```

2. **Set up environment variables**:
   Create a `.env` file in the root directory and add your environment variables:
   ```bash
   MONGO_INITDB_ROOT_USERNAME=yourMongoUsername
   MONGO_INITDB_ROOT_PASSWORD=yourMongoPassword
   MONGO_DB_USERNAME=yourMongoAppUsername
   MONGO_DB_PASSWORD=yourMongoAppPassword
   DOCKER_HUB_USERNAME=yourDockerHubUsername
   DOCKER_HUB_TOKEN=yourDockerHubAccessToken
   ```

   These variables allow you to securely pass sensitive data (like passwords) to your services without hardcoding them in your app.

3. **Build and run the project**:
   To start all the services, run:
   ```bash
   docker-compose up --build
   ```

   This command will:
   - Build the Docker images.
   - Start the MongoDB service.
   - Start the Node.js app.
   - Start NGINX to route traffic.

4. **Access the services**:
   - **Mongo Express** (MongoDB GUI): `http://localhost:8081`
   - **NGINX**: `http://localhost:80`

---

## Understanding the GitHub Actions Workflow

This repository uses **GitHub Actions** to automate the process of building and pushing the Docker image to Docker Hub.

### How It Works

Whenever you push changes to the `master` branch:
- GitHub Actions pulls the latest code.
- It builds the Node.js app into a Docker image.
- The image is then pushed to Docker Hub using your Docker Hub credentials.

This keeps your image up to date with every code change and makes it easy to deploy anywhere Docker is supported.

---

## Breaking Down the Docker Components

### Node.js Application

Your Node.js app is packaged into a Docker image. The `Dockerfile` in the project tells Docker how to set up the environment, install dependencies, and run the app.

### MongoDB

MongoDB runs as a separate service inside its own container. This service stores all the data for your app. Since it runs independently from the Node.js app, they can communicate over a network, which means MongoDB can be swapped out or scaled without affecting the app.

### NGINX

NGINX is set up as a **reverse proxy**. It listens for incoming traffic and directs it to the appropriate service—in this case, your Node.js app. This makes your app scalable and efficient, especially if you’re running multiple instances of the Node.js service.

---

## Docker Compose: Bringing Everything Together

Docker Compose is a tool that helps you manage multiple Docker containers. The `docker-compose.yml` file describes all the services that make up your app and how they should interact.

### What's in the Docker Compose File?

- **MongoDB**: A NoSQL database to store your app's data.
- **Mongo Express**: A GUI for managing your MongoDB.
- **Node.js app**: The main service that handles all backend logic.
- **NGINX**: The reverse proxy that directs incoming traffic.

You can easily start, stop, and scale all these services with just a few commands using Docker Compose.

---

## Key Concepts Explained

### Service Isolation

Each part of your app (Node.js, MongoDB, etc.) runs in its own container. This means they are isolated from one another. If one service fails, the others can keep running.

### Scaling

With microservices, you can scale individual services based on the load. For example, if your Node.js app needs more processing power, you can run multiple instances of it, while MongoDB and NGINX remain unaffected.

### Reverse Proxy with NGINX

NGINX acts as a **reverse proxy** that sits in front of your services. It takes incoming requests and forwards them to the right service (in this case, the Node.js app). If you're running multiple copies of the Node.js app, NGINX can also balance the load between them.

### Environment Variables

Environment variables store sensitive data (like database usernames and passwords) outside the code. This keeps your credentials safe and makes your app easier to configure in different environments.

---

## Contributing

We welcome contributions! If you have any ideas or spot any issues, feel free to fork this repository, make changes, and submit a pull request.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
