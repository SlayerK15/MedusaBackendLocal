*Medusa Backend Server Setup Locally
**Prerequisites
**Ensure the following are installed and configured on your system before setting up the Medusa backend server:
1.	Node.js (Ensure it is installed globally)
2.	Yarn (Install globally)
3.	PostgreSQL (Database server installed and configured)
4.	Medusa CLI (Install globally using npm install -g @medusajs/medusa)
5.	Redis (Optional but recommended as it is used as a cache)

  


Steps to Set Up Medusa Backend
Step 1: Create a Medusa Project Using CLI
Run the following commands to set up a Medusa project:
medusa new samplestore
cd samplestore

  
Step 1.b
Configuring the Postgre database while creating the backend

 
 
Step 1c: Install Dependencies
Inside the project directory, install the necessary dependencies:
npm install

 

 
Step 1d: Set Up Environment Variables
Configure or modify the environment variables by creating or editing the .env file. This will set up the database and other required configurations for the web app.
 

Step 1e: Create a Superuser
Create a superuser to access the backend portal using the following command:
medusa user -e admin@example.com -p password123

 

Step 2 (Optional): Run Redis Server
If you have Redis installed, run the Redis server for caching purposes.
redis-server

Step 2b: Seed Data (Optional)
You can seed sample data into the database (optional but useful for testing).

 

 
Step 3: Run the Medusa Server
To start the Medusa server, run:
medusa develop
This will set up the Medusa backend server locally. You can now start building your commerce platform or modify the project as neede  d. 
 

 
Output
The Medusa application launches a GUI on the port http://localhost:7001, which can be accessed using the superuser created earlier.
  


Seeded Data From the seeding Process
 

References
For more detailed information, visit the official Medusa documentation:
MedusaJS Local Development Guide

