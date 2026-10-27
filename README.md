# 3-Tier DevSecOps Project

A full-stack CRUD application deployed using Docker and Docker Compose, with a React frontend, Node.js backend, and MySQL database.

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Installation and Setup](#installation-and-setup)
- [Access the Application](#access-the-application)
- [Docker Commands](#docker-commands)
- [Security Notes](#security-notes)
- [Troubleshooting](#troubleshooting)

## Project Overview

This project demonstrates how to run a three-tier web application using containerization.

The application separates the frontend, backend, and database into different services. Docker Compose manages the services and their configuration.

### Key Features

- React-based frontend
- Node.js backend API
- MySQL database
- Docker-based application containerization
- Docker Compose orchestration
- Environment variables for sensitive configuration
- Persistent MySQL storage using a Docker volume

## Architecture

```text
                User / Browser
                      |
                      v
             React Frontend
              localhost:3000
                      |
                      v
             Node.js Backend
              localhost:5000
                      |
                      v
                MySQL Database
             Docker internal network
                Container: 3306
                Host: 3307
```

The frontend communicates with the backend API, and the backend connects to MySQL to store and retrieve application data.

## Technologies Used

| Technology | Purpose |
|---|---|
| React.js | Frontend user interface |
| Node.js | Backend runtime |
| Express.js | Backend API framework, if used |
| MySQL 8 | Relational database |
| Docker | Containerization |
| Docker Compose | Multi-container application management |
| Git | Version control |
| GitHub | Source code hosting |

## Prerequisites

Install the following tools before running the project:

- Git
- Docker Desktop
- Visual Studio Code (recommended)

Ensure Docker Desktop is running.

Verify the installations:

```powershell
git --version
docker --version
docker compose version
```

## Project Structure

```text
3-Tier-DevSecOps-Project/
├── api/                 # Backend application
├── client/              # Frontend application
├── mysql-init/          # Database initialization scripts
├── docker-compose.yaml  # Docker Compose configuration
├── .gitignore           # Files excluded from Git
└── README.md            # Project documentation
```

The exact files and folders may differ depending on your repository.

## Configuration

The project uses environment variables to configure database credentials and the JWT secret.

Create a `.env` file in the project root, next to `docker-compose.yaml`.

Example:

```dotenv
MYSQL_ROOT_PASSWORD=replace_with_a_strong_password
JWT_SECRET=replace_with_a_long_random_secret
```

Use your own strong values. Do not commit `.env` files or real credentials to GitHub.

Make sure `api/.env` and `client/.env` are also excluded from Git if they contain private values.

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/Lokeshvallapu/Lokesh-3-Tier-DevSecOps-Project.git
cd Lokesh-3-Tier-DevSecOps-Project
```

### 2. Configure environment variables

Create the root `.env` file using the configuration described above.

### 3. Build and start the application

```bash
docker compose up -d --build
```

This command builds the required images and starts the services in the background.

### 4. Check running containers

```bash
docker compose ps
```

### 5. View application logs

```bash
docker compose logs -f
```

Press `Ctrl+C` to stop following the logs. This does not stop the containers.

## Access the Application

After the services start successfully:

- **Frontend:** http://localhost:3000
- **Backend:** http://localhost:5000

The backend URL is the service address; the exact API endpoints depend on the routes implemented in the application.

## Docker Commands

Start services:

```bash
docker compose up -d
```

Rebuild and start:

```bash
docker compose up -d --build
```

Check services:

```bash
docker compose ps
```

View logs:

```bash
docker compose logs -f
```

Stop services without deleting persistent database data:

```bash
docker compose down
```

## Security Notes

- Never upload passwords, API keys, JWT secrets, or private environment files to GitHub.
- Use `.env.example` to document required variables without exposing real values.
- Rotate credentials that have previously been exposed.
- Keep the MySQL database port restricted to the local machine unless external access is specifically required.
- Use HTTPS, proper authentication, and secure production configurations before deploying publicly.

## Troubleshooting

### Containers are not starting

```bash
docker compose ps
docker compose logs
```

Check the logs for configuration errors, failed health checks, or port conflicts.

### Environment variables are missing

Confirm that the root `.env` file exists and contains both required variables.

### Database connection errors

Check that the MySQL service is running, that the backend uses the correct database hostname (`mysql` inside the Compose network), and that the database credentials match.

### Frontend cannot reach the backend

Verify the backend API URL and confirm that the API is accessible from the frontend's runtime environment.

## Author

**Lokesh Vallapu**

GitHub: https://github.com/Lokeshvallapu

LinkedIn: https://www.linkedin.com/in/vallapulokesh/
