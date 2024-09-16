# Medusa Backend Deployment on AWS EC2

This project contains the steps to deploy the Medusa eCommerce backend on an AWS EC2 instance using Docker and Docker Compose.

## Prerequisites

Before you begin, ensure you have the following:

- AWS account
- EC2 instance running **Ubuntu 22.04**
- Docker and Docker Compose installed
- Git installed
- Public and private SSH key pair for connecting to the EC2 instance

## Steps for Deployment

### 1. Login to AWS EC2 Dashboard

Log in to your AWS account and navigate to the EC2 dashboard.

### 2. Create a New Key Pair

Create a new key pair from the EC2 dashboard, which will allow you to SSH into your virtual machine. Store this key pair safely on your local machine.

### 3. Launch an EC2 Instance

- Launch a new EC2 instance running **Ubuntu 22.04**.
- Select an instance type that provides sufficient compute power for your application (e.g., t2.small).
- Attach the previously created key pair to this instance.

### 4. Configure Security Groups

Modify the security groups of your EC2 instance to allow incoming traffic on **port 9000**. This will allow external access to the Medusa backend.

### 5. SSH into the EC2 Instance

After your instance is running, access it via SSH with the following command:

```bash
ssh -i /path/to/your/key.pem ubuntu@<YOUR_EC2_IP>
```

Replace `/path/to/your/key.pem` with the path to your key pair and `<YOUR_EC2_IP>` with the public IP address of your EC2 instance.

### 6. Install Docker, Docker Compose, and Git

Once you're inside the EC2 instance, update the package manager and install Docker, Docker Compose, and Git:

```bash
sudo apt update
sudo apt install -y docker.io docker-compose git
```

### 7. Clone the Medusa Backend Repository

Clone the Medusa backend repository from the Task 2 branch using Git:

```bash
git clone -b Task-2 https://github.com/SlayerK15/MedusaBackendLocal.git
cd MedusaBackendLocal
```

### 8. Configure Environment Variables

Create a `.env` file in the root directory of the cloned project to store environment variables required by the application. Example:

```bash
JWT_SECRET=something
COOKIE_SECRET=something
DATABASE_URL=postgres://postgres:123@postgres:5432/medusa_store_db
REDIS_URL=redis://localhost:6379
NODE_ENV=production
```

### 9. Modify the Dockerfile

In the `Dockerfile`, ensure that Medusa migrations run before the server starts. Modify the `CMD` section as follows:

```Dockerfile
CMD ["sh", "-c", "medusa migrations run && medusa start"]
```

This change ensures that database migrations are applied automatically during the application startup.

### 10. Build and Launch the Application

Build the Docker containers for the Medusa backend and PostgreSQL services using Docker Compose:

```bash
docker-compose up --build
```

Once the build is complete, launch the application in detached mode:

```bash
docker-compose up -d
```

### 11. Verify the Application

Check if the Medusa backend is running by navigating to:

```
http://<YOUR_EC2_IP>:9000/app
```

You should see the Medusa application interface.

### 12. Create the Admin User

Log in to the EC2 instance using the "Connect" option in the AWS console or SSH, and create an initial admin user via the terminal.

### 13. Login to the Admin Panel

Once the admin user is created, log in to the Medusa backend by navigating to:

```
http://<YOUR_EC2_IP>:9000/app/login
```

Enter the credentials for the admin user to access the admin panel.

### 14. Managing the Application

You can manage the application using Docker commands. For example:

- To stop the application:
  ```bash
  docker-compose down
  ```

- To check logs:
  ```bash
  docker-compose logs
  ```

- To restart the application:
  ```bash
  docker-compose restart
  ```