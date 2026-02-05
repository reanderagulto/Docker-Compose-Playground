# Docker Compose Fullstack Web Application Template

This is a basic Docker Compose template for building fullstack web applications with frontend and backend services. The template provides a simple starting point for developing modern web applications with containerization.

## Architecture

### Services

1. **Frontend** - React + Vite application
   - Built with React 18
   - Vite as build tool and dev server
   - Dockerized with multi-stage builds
   - Runs on port 3000

2. **Backend** - Node.js + Express API
   - Express.js web framework
   - Dockerized with Node.js 18
   - Runs on port 5000

### Communication

- Frontend makes API calls to the backend using relative paths
- Services are connected through Docker network
- CORS is configured for cross-origin requests

## Getting Started

### Prerequisites

- Docker installed on your machine
- Docker Compose (usually included with Docker Desktop)

### Setup

1. Clone or download this repository
2. Copy the `.env.example` file to `.env` and configure if needed
3. Build and start the services:

```bash
# Build and start containers in detached mode
docker-compose up -d

# View logs
docker-compose logs -f

# Stop containers
docker-compose down

# Restart containers
docker-compose restart

# Rebuild and start (if you made changes to Dockerfiles)
docker-compose up -d --build
```

### Accessing the Application

- Frontend: http://localhost:3000
- Backend API: http://localhost:5000

## Development

### Frontend Development

```bash
cd frontend
npm install
npm run dev
```

### Backend Development

```bash
cd backend
npm install
npm run dev
```

### Docker Development

Both services support hot reload for development:

- Frontend (Vite): Hot module replacement enabled
- Backend (Node.js): Nodemon watches for changes

## Project Structure

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

## Docker Configuration

### Frontend Dockerfile

- Uses Node.js 18 for development
- Multi-stage build for production optimization
- Serves static files with Nginx in production

### Backend Dockerfile

- Uses Node.js 18
- Installs dependencies
- Exposes port 5000
- Health check endpoint for monitoring

### Docker Compose

- Configures both services
- Network configuration
- Volume mounting for hot reload
- Port mapping
- Health check configuration

## Scripts

### Frontend

```json
"scripts": {
  "dev": "vite",           // Start development server
  "build": "vite build",   // Build for production
  "preview": "vite preview" // Preview production build
}
```

### Backend

```json
"scripts": {
  "dev": "nodemon index.js",  // Development with hot reload
  "start": "node index.js"    // Production start
}
```

## Health Check

Both services include health check endpoints:

- Frontend: `/` (returns 200 OK)
- Backend: `/api/health` (returns JSON with status)

## Customization

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

**Frontend:**

```bash
cd frontend
npm install <package-name>
```

**Backend:**

```bash
cd backend
npm install <package-name>
```

## Production Deployment

For production deployment:

1. Build the services with production configuration
2. Use appropriate environment variables
3. Configure reverse proxy (e.g., Nginx)
4. Set up SSL certificates
5. Add monitoring and logging

## Best Practices

1. Keep dependencies minimal
2. Use environment variables for configuration
3. Implement proper error handling
4. Add testing to both services
5. Optimize container sizes
6. Use health checks for monitoring
7. Implement proper logging
8. Secure your API endpoints

## License

MIT
