<div align="center">

<br/>

# 🍽️ My Canteen Application

### Production-Ready · 3-Tier MERN Stack · Fully Dockerized · EC2 Deployed

<br/>

![Live](https://img.shields.io/badge/Status-Live%20%F0%9F%9F%A2-brightgreen?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=flat-square&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-Reverse%20Proxy-009639?style=flat-square&logo=nginx&logoColor=white)
![Node](https://img.shields.io/badge/Node.js-Backend-339933?style=flat-square&logo=node.js&logoColor=white)
![React](https://img.shields.io/badge/React-Frontend-61DAFB?style=flat-square&logo=react&logoColor=black)
![MongoDB](https://img.shields.io/badge/MongoDB-6.0-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-Payments-635BFF?style=flat-square&logo=stripe&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-Media-3448C5?style=flat-square&logo=cloudinary&logoColor=white)

<br/>

> A fully containerized, production-grade  canteen_application —
> built with the MERN stack, secured behind Nginx, and shipped via Docker Compose.

<br/>

### 🌐 [Live Demo → http://15.207.108.154:3000/](http://15.207.108.154:3000/)

<br/>

</div>

---

## 📌 Table of Contents

- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Key Features](#-key-features)
- [Project Structure](#-project-structure)
- [Docker Setup](#-docker-setup)
- [Nginx Configuration](#-nginx-configuration)
- [Environment Variables](#-environment-variables)
- [Health Checks](#-health-checks)
- [Running Locally](#-running-locally)
- [Author](#-author)

---

## 🏛️ Architecture

```
                     ┌───────────────────────────────┐
                     │       User / Admin             │
                     │         Browser                │
                     └──────────────┬────────────────┘
                                    │ HTTP
                                    ▼
                     ┌───────────────────────────────┐
                     │      🌐  Nginx  :80            │
                     │       Reverse Proxy            │
                     │    Single Entry Point          │
                     └────┬──────────┬───────────┬───┘
                          │  /       │  /api      │  /admin
                          ▼          ▼            ▼
               ┌──────────────┐  ┌──────────┐  ┌──────────────┐
               │  🖥 Frontend  │  │ ⚙ Backend │  │ 🛠 Admin Panel│
               │  React SPA   │  │ Express  │  │  React SPA   │
               │  Port 3000   │  │ Port 5000│  │  Port 3001   │
               └──────────────┘  └────┬─────┘  └──────────────┘
                                       │
                                       ▼
                              ┌─────────────────┐
                              │   🗄 MongoDB 6.0  │
                              │  Named Volume    │
                              │   Port 27017     │
                              └─────────────────┘
```

> All services run in **isolated Docker containers** connected via a custom bridge network `mca_network`.

---

## ⚙️ Tech Stack

| Layer | Technology | Role |
|-------|-----------|------|
| 🖥️ Frontend | React.js | User-facing SPA |
| 🛠️ Admin | React.js | Admin dashboard SPA |
| ⚙️ Backend | Node.js + Express.js | REST API server |
| 🗄️ Database | MongoDB 6.0 | NoSQL persistent storage |
| 🌐 Proxy | Nginx | Reverse proxy + routing |
| 🐳 Container | Docker + Docker Compose | Orchestration |
| ☁️ Media | Cloudinary | Image/file storage |
| 💳 Payments | Stripe | Payment gateway |
| 📧 Email | SMTP (Gmail) | Transactional emails |
| 🔐 Auth | JWT + HTTP Cookies | Stateless authentication |
| ☁️ Cloud | AWS EC2 | Production server |

---

## 🔥 Key Features

### 🌐 Nginx Reverse Proxy
- `/` → **Frontend** (React user app)
- `/api/*` → **Backend** (Express REST API)
- `/admin` → **Admin Panel** (React admin app)
- One port exposed, clean and secure routing

### 🐳 Dockerized Microservices
- Each service has its own optimized **Dockerfile**
- **Multi-stage builds** — small, production-only images
- **Non-root users** inside every container (security best practice)
- All containers auto-restart with `restart: unless-stopped`

### 🔄 Docker Compose Orchestration
- One command to bring up the **entire stack**
- `depends_on` with `condition: service_healthy` — services start in correct order
- Named volume `mca_mongo_data` — MongoDB data **persists** across restarts
- Custom bridge network `mca_network` — services communicate by container name

### 🔐 Security
- JWT-based stateless auth with cookie support
- All secrets via environment variables — zero hardcoding
- Non-root container users
- Nginx as single gateway — backend never exposed directly

### ✅ Production Ready
- Health checks on MongoDB and Backend
- Clean separation of concerns across services
- Scalable architecture — ready for Kubernetes migration

---

## 📁 Project Structure

```
canteen_application_deployment/
│
├── 📂 admin/                    # Admin Panel — React SPA
│   ├── Dockerfile               # Multi-stage build
│   └── src/
│
├── 📂 backend/                  # REST API — Node.js + Express
│   ├── Dockerfile               # Multi-stage build
│   └── src/
│       ├── routes/              # API endpoints
│       ├── controllers/         # Business logic
│       ├── models/              # MongoDB schemas
│       └── middleware/          # Auth + error handling
│
├── 📂 frontend/                 # User Frontend — React SPA
│   ├── Dockerfile               # Multi-stage build
│   └── src/
│
├── 📂 nginx/                    # Nginx reverse proxy
│   └── nginx.conf               # Routing configuration
│
├── 📄 docker-compose.yml        # Full-stack orchestration
├── 📄 .gitignore
└── 📄 README.md
```

---

## 🐳 Docker Setup

### Build & Start All Services

```bash
docker-compose up -d --build
```

### Other Commands

```bash
# View all running containers
docker ps

# Stream logs for backend
docker-compose logs -f backend

# Stop all services
docker-compose down

# Stop and remove volumes (clean slate)
docker-compose down -v

# Rebuild a single service
docker-compose up -d --build backend

# Check resource usage
docker stats
```

### Service URLs

| Service | URL |
|---------|-----|
| 🖥️ Frontend | http://localhost:3000 |
| 🛠️ Admin Panel | http://localhost:3001 |
| ⚙️ Backend API | http://localhost:5000 |
| 🗄️ MongoDB | mongodb://localhost:27017 |

---

---

## 🔐 Environment Variables

Create a `.env` file in the project root — **never commit this file**:

```env
# MongoDB
MONGO_INITDB_ROOT_USERNAME=admin
MONGO_INITDB_ROOT_PASSWORD=root123
MONGODB_URI=mongodb://admin:root123@mongo:27017/mca_db

# JWT & Cookies
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRE=7d
COOKIE_EXPIRE=7

# Cloudinary
CLOUDINARY_NAME=your_cloud_name
CLOUDINARY_KEY=your_cloudinary_key
CLOUDINARY_SECRET=your_cloudinary_secret

# Stripe
STRIPE_SECRET=your_stripe_secret_key

# SMTP (Gmail)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=465
SMTP_SERVICE=gmail
SMTP_USER=mycanteen.in@gmail.com
SMTP_PASSWORD=your_app_password

# App
NODE_ENV=production
PORT=5000
```

> ⚠️ Add `.env` to `.gitignore`. Use **GitHub Secrets** for CI/CD pipelines and **AWS Parameter Store** for production.

---

## 📊 Health Checks

All critical services have health checks configured in `docker-compose.yml`:

| Service | Health Check Command | Interval | Retries |
|---------|---------------------|----------|---------|
| 🗄️ MongoDB | `mongosh --eval "db.adminCommand('ping')"` | 30s | 5 |
| ⚙️ Backend | `wget -qO- http://localhost:5000/` | 30s | 5 |
| 🖥️ Frontend | `condition: service_healthy` (waits for backend) | — | — |
| 🛠️ Admin | `condition: service_healthy` (waits for backend) | — | — |

---


---

### Option 1 — Docker Compose ✅ Recommended

```bash
# Clone repo
https://github.com/biswajit7815/canteen_application_deployment.git
cd canteen_application_deployment.git

# Setup environment
cp .env.example .env
# Fill in your values in .env

# Start everything
docker-compose up --build
```

### Option 2 — Manual (Without Docker)

```bash
# Terminal 1 — Backend
cd backend && npm install && npm start

# Terminal 2 — Frontend
cd frontend && npm install && npm start

# Terminal 3 — Admin
cd admin && npm install && npm start
```

---

---

## 👨‍💻 Author

**Biswajit** — DevOps & Full Stack Engineer

[![GitHub](https://img.shields.io/badge/GitHub-biswajit7815-181717?style=flat-square&logo=github)](https://github.com/biswajit7815)

> Forked from [asit-sahoo-28/FinalYear-Project-My-Canteen-application](https://github.com/asit-sahoo-28/FinalYear-Project-My-Canteen-application)

---

<div align="center">

![Docker](https://img.shields.io/badge/Built%20with-Docker-2496ED?style=flat-square&logo=docker)
![AWS](https://img.shields.io/badge/Hosted%20on-AWS%20EC2-FF9900?style=flat-square&logo=amazonaws)
![MongoDB](https://img.shields.io/badge/Database-MongoDB-47A248?style=flat-square&logo=mongodb)
![Nginx](https://img.shields.io/badge/Proxy-Nginx-009639?style=flat-square&logo=nginx)

<br/>

⭐ **Star this repo if it helped you!**

</div>
