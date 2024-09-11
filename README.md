# Containerizing and Running Medusa Backend Locally Using Docker

This documentation will guide you through the steps to containerize and run the Medusa backend with PostgreSQL using Docker. It also includes instructions to access the Admin GUI and check the health of the service.

## Prerequisites
1. Docker and Docker Compose installed on your machine.
2. Basic knowledge of Medusa.js, Node.js, and PostgreSQL.

## Step 1: Cloning the Git Repository

Clone the repository of Task 1 to your local machine:

```bash
git clone https://github.com/SlayerK15/MedusaBackendLocal.git
```

## Step 2: Dockerfile Setup

Here’s the Dockerfile used to containerize the Medusa backend:

```Dockerfile
FROM node:18-alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install -g @medusajs/medusa
RUN npm install
COPY . .
EXPOSE 9000
CMD [ "medusa", "start" ]
```

## Step 3: docker-compose.yml Setup

Here is the `docker-compose.yml` file, which defines two services: Medusa (backend) and PostgreSQL (database).

```yaml
services:
  medusa:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: samplestore
    ports:
      - "9000:9000"
    depends_on:
      - postgres
    environment:
      DATABASE_URL: postgres://postgres:123@postgres:5432/medusa_store_db

  postgres:
    image: postgres:14
    environment:
      POSTGRES_DB: medusa_store_db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: 123
    volumes:
      - pg_data:/var/lib/postgresql/data

volumes:
  pg_data:
    driver: local
```

### Medusa Service:
- Builds the backend image from the Dockerfile.
- Maps **port 9000** for backend access.
- Sets the `DATABASE_URL` environment variable to connect to PostgreSQL.

### Postgres Service:
- Runs PostgreSQL 14.
- Configured with a database name, user, and password.
- Uses a volume `pg_data` to ensure database persistence.

## Step 4: Running the Application

### a. Build and Run the Containers:

Navigate to the directory containing your `Dockerfile` and `docker-compose.yml` file, then run:

```bash
docker-compose up --build
```

This will build and start both the Medusa backend and PostgreSQL database.

### b. Verify the Setup:

Check if the services are running:

```bash
docker ps
```

The Medusa backend should be running on `localhost:9000`.

## Step 5: Accessing the Medusa Admin GUI

### Open the Admin GUI:
- Go to `http://localhost:9000/app` in your browser to access the Medusa Admin interface.

### Login:
- Use the credentials you created during Medusa setup.
- Once logged in, you will have access to manage products, customers, and orders through the admin panel.

## Step 6: Checking Backend Health

### Health Check:
To ensure that your Medusa backend is running smoothly, perform a health check by navigating to:

```
http://localhost:9000/health
```

The endpoint should return:
```json
{
  "status": "OK"
}
```

## Admin User Creation (Optional)

If you need to create an admin user, you can do so by running the following command in your Medusa container:

```bash
docker exec -it samplestore medusa user --create
```

## Stopping the Containers

To stop the containers when you're done, simply run:

```bash
docker-compose down
```

## Admin GUI Screenshots

Include relevant screenshots of the Medusa Admin GUI to document how to log in and manage the system.

---

This setup ensures a consistent and isolated development environment that can be easily deployed across different machines.
