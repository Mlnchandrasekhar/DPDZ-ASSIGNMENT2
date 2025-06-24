
# DevOps Internship Assignment - Nginx Reverse Proxy + Docker

This project sets up a multi-service Docker environment with an Nginx reverse proxy that routes requests to two backend services — a Go application and a Python application — using `docker-compose`.

---

## 🚀 Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/devops-assignment.git
   cd devops-assignment
   ```

2. **Make sure Docker and Docker Compose are installed**

   - Install Docker: https://docs.docker.com/get-docker/
   - Install Docker Compose: https://docs.docker.com/compose/install/

3. **Build and Run the Project**
   ```bash
   docker-compose up --build
   ```

4. **Test in browser or with curl**
   ```bash
   curl http://localhost:8080/service1/health
   curl http://localhost:8080/service2/health
   ```

---

## 🌐 How Routing Works

The project uses **Nginx** as a reverse proxy to route HTTP traffic to two separate backend services based on the request path.

- `localhost:8080/service1` → forwards to Go backend (`service_1`)
- `localhost:8080/service2` → forwards to Python backend (`service_2`)

### 📦 Nginx Configuration (nginx.conf)

```nginx
location /service1/ {
    proxy_pass http://service_1:8001/;
    access_log /var/log/nginx/access.log combined;
}

location /service2/ {
    proxy_pass http://service_2:8002/;
    access_log /var/log/nginx/access.log combined;
}
```

- All requests go through **Nginx container** on port `8080`.
- Nginx uses **bridge network** to route to internal container services.
- Incoming request paths are used to determine the backend destination.

---

## 📁 Project Structure

```
.
├── docker-compose.yml
├── nginx
│   ├── nginx.conf
│   └── Dockerfile
├── service_1
│   └── Dockerfile
├── service_2
│   └── Dockerfile
└── README.md
```

---

