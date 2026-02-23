## Docker Setup Instructions

### Prerequisites

Ensure the following are installed:

* Docker ≥ 24
* Docker Compose ≥ 2
* Git

Verify installation:

```bash
docker --version
docker compose version
```

---

### Step 1 — Clone Repository

```bash
git clone <repository-url>
cd <project-root>
```

---

### Step 2 — Configure Environment Variables

Create a `.env` file in the project root:

```env
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=department_db
MYSQL_USER=appuser
MYSQL_PASSWORD=apppass

RABBITMQ_DEFAULT_USER=guest
RABBITMQ_DEFAULT_PASS=guest

JWT_SECRET=your_secret_key
```

Adjust values as needed.

---

### Step 3 — Build All Services

From project root:

```bash
docker compose build
```

This will:

* build each microservice image
* install dependencies
* package Spring Boot apps

---

### Step 4 — Start System

```bash
docker compose up
```

To run in background:

```bash
docker compose up -d
```

---

### Step 5 — Verify Services

Check running containers:

```bash
docker ps
```

### Step 6 — Stop System

```bash
docker compose down
```

Remove volumes too:

```bash
docker compose down -v
```

---

### Services Overview

| Service            | Port  |
| ------------------ | ----- |
| Auth Service       | 8081  |
| Employee Service   | 8082  |
| Department Service | 8084  |
| Leave Service      | 8085  |
| MySQL              | 3306  |
| RabbitMQ           | 5672  |
| RabbitMQ UI        | 15672 |

---

### Rebuild After Code Changes

If you modify code:

```bash
docker compose down
docker compose build
docker compose up
```

---

### Logs

View logs of specific service:

```bash
docker compose logs department-service
```

Follow logs live:

```bash
docker compose logs -f department-service
```

---

### Troubleshooting

**Port already in use**

```
Error: bind: address already in use
```

Solution: stop process using port or change port in compose file.

---

**Database connection failed**

* ensure MySQL container is running
* check credentials in `.env`

---

**RabbitMQ connection error**

* verify host = `rabbitmq`
* not `localhost` (inside containers)

---

### Clean Reset (Fresh Start)

Removes all containers, volumes, images:

```bash
docker compose down -v
docker system prune -a
```
