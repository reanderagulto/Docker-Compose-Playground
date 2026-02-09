# 🚀 Fullstack Web Application Template

[![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express.js-404D59?style=for-the-badge)](https://expressjs.com/)

A modern, production-ready fullstack web application template built with Docker Compose, featuring a React frontend and Node.js/Express backend.

## 📋 Table of Contents

- [🚀 Fullstack Web Application Template](#-fullstack-web-application-template)
- [📋 Table of Contents](#-table-of-contents)
- [🏗️ Architecture](#️-architecture)
  - [Services](#services)
  - [Communication](#communication)
- [🛠️ Getting Started](#️-getting-started)
  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
  - [Accessing the Application](#accessing-the-application)
- [💻 Development](#-development)
  - [Frontend Development](#frontend-development)
  - [Backend Development](#backend-development)
  - [Docker Development](#docker-development)
- [📁 Project Structure](#-project-structure)
- [🐳 Docker Configuration](#-docker-configuration)
  - [Frontend Dockerfile](#frontend-dockerfile)
  - [Backend Dockerfile](#backend-dockerfile)
  - [Docker Compose](#docker-compose)
- [📜 Scripts](#-scripts)
  - [Frontend Scripts](#frontend-scripts)
  - [Backend Scripts](#backend-scripts)
- [❤️ Health Check](#️-health-check)
- [⚙️ Customization](#️-customization)
  - [Environment Variables](#environment-variables)
  - [Adding Dependencies](#adding-dependencies)
- [🚀 Production Deployment](#-production-deployment)
- [✨ Best Practices](#-best-practices)
- [📄 License](#-license)

## 🏗️ Architecture

### Services

#### 🎨 Frontend

- **React 18** - Modern UI library
- **Vite** - Lightning-fast build tool and dev server
- **Dockerized** with multi-stage builds
- Runs on **port 3000**
- Hot module replacement for rapid development

#### 🚀 Backend

- **Express.js** - Minimalist web framework
- **Node.js 18** - JavaScript runtime
- **Dockerized** for consistency
- Runs on **port 5000**
- Nodemon for hot reload during development

### Communication

- Frontend makes API calls using relative paths
- Services connected through Docker network
- CORS configured for cross-origin requests
- Environment variables for flexible configuration

## 🛠️ Getting Started

### Prerequisites

📦 **Docker** - Containerization platform  
🐳 **Docker Compose** - Multi-container orchestration (included with Docker Desktop)

### Setup

1. **Clone or download this repository**
2. **Copy environment variables**
   ```bash
   cp .env.example .env
   ```
3. **Build and start services**

   ```bash
   # Build and start containers in detached mode
   docker-compose up -d

   # View real-time logs
   docker-compose logs -f

   # Stop containers
   docker-compose down

   # Restart containers
   docker-compose restart

   # Rebuild and start (after Dockerfile changes)
   docker-compose up -d --build
   ```

### Accessing the Application

🌐 **Frontend**: http://localhost:3000  
🔌 **Backend API**: http://localhost:5000

## 💻 Development

### Frontend Development

```bash
cd frontend
npm install
npm run dev
```

Features hot module replacement and Vite's lightning-fast dev server.

### Backend Development

```bash
cd backend
npm install
npm run dev
```

Uses Nodemon to automatically restart on file changes.

### Docker Development

Both services support hot reload:

- **Frontend**: Vite HMR enabled
- **Backend**: Nodemon watches for changes
- Volumes mounted for real-time code updates

## 📁 Project Structure

```
fullstack-docker-compose/
├── .env.example          # Environment variables template
├── .gitignore           # Git ignore rules
├── docker-compose.yml   # Docker Compose configuration
├── README.md            # This file
├── frontend/            # React + Vite application
│   ├── Dockerfile       # Frontend Docker configuration
│   ├── package.json     # Frontend dependencies
│   ├── vite.config.js   # Vite configuration
│   ├── index.html       # Entry HTML file
│   └── src/             # React application source
└── backend/             # Node.js + Express API
    ├── Dockerfile       # Backend Docker configuration
    ├── package.json     # Backend dependencies
    └── index.js         # Express server entry point
```

## 🐳 Docker Configuration

### Frontend Dockerfile

- **Development**: Node.js 18 with Vite dev server
- **Production**: Multi-stage build with Nginx for static file serving
- Optimized for minimal container size
- Health check endpoint at `/`

### Backend Dockerfile

- **Node.js 18** runtime
- Dependencies installed in separate layer for caching
- Port 5000 exposed
- Health check endpoint at `/api/health`
- Production-ready configuration

### Docker Compose

- Network configuration for service communication
- Volume mounting for hot reload
- Port mapping (3000 → frontend, 5000 → backend)
- Health check monitoring
- Environment variable support

## 📜 Scripts

### Frontend Scripts

```json
"scripts": {
  "dev": "vite",           // Start development server (HMR enabled)
  "build": "vite build",   // Build for production (optimized)
  "preview": "vite preview" // Preview production build locally
}
```

### Backend Scripts

```json
"scripts": {
  "dev": "nodemon index.js",  // Development with hot reload
  "start": "node index.js"    // Production start
}
```

## ❤️ Health Check

Both services include health check endpoints:

- **Frontend**: `GET /` → Returns 200 OK
- **Backend**: `GET /api/health` → Returns JSON status:
  ```json
  {
    "status": "ok",
    "timestamp": "2024-01-01T00:00:00.000Z"
  }
  ```

## ⚙️ Customization

### Environment Variables

Create a `.env` file based on `.env.example` and customize:

```env
# Frontend
VITE_API_URL=http://localhost:5000

# Backend
PORT=5000
NODE_ENV=development
```

### Adding Dependencies

#### Frontend

```bash
cd frontend
npm install <package-name>
```

#### Backend

```bash
cd backend
npm install <package-name>
```

## 🚀 Production Deployment

For production environments:

1. Build services with production configuration
2. Use appropriate environment variables
3. Configure reverse proxy (e.g., Nginx)
4. Set up SSL certificates (Let's Encrypt)
5. Add monitoring and logging (Prometheus, Grafana)
6. Implement load balancing
7. Set up CI/CD pipeline

## ✨ Best Practices

✅ **Keep dependencies minimal** - Only install what you need  
✅ **Use environment variables** - For configuration and secrets  
✅ **Implement proper error handling** - Centralized error middleware  
✅ **Add testing** - Unit, integration, and E2E tests  
✅ **Optimize container sizes** - Multi-stage builds, minimal base images  
✅ **Use health checks** - For monitoring and auto-healing  
✅ **Implement proper logging** - Structured logging with Winston or Pino  
✅ **Secure your API endpoints** - Authentication, authorization, rate limiting  
✅ **Code linting and formatting** - ESLint, Prettier, Husky pre-commit hooks  
✅ **Documentation** - Keep README and API docs up to date

## 📄 License

MIT License - Feel free to use this template for your projects!

---

⭐ **If you find this template useful, please give it a star!**
