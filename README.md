<h1>Medusa Backend Server Setup Locally</h1>
<h3>Prerequisites</h3>
Ensure the following are installed and configured on your system before setting up the Medusa backend server:

1.	Node.js (Ensure it is installed globally)
2.	Yarn (Install globally)
3.	PostgreSQL (Database server installed and configured)
4.	Medusa CLI (Install globally using npm install -g @medusajs/medusa)
5.	Redis (Optional but recommended as it is used as a cache)

  
<h3>Steps to Set Up Medusa Backend</h3>
<hr>
<h3>Step 1: Create a Medusa Project Using CLI</h3>
Run the following commands to set up a Medusa project:
medusa new samplestore
cd samplestore

<h3>Step 2:</h3>
Configuring the Postgre database while creating the backend

<h3>Step 3: Install Dependencies</h3>
Inside the project directory, install the necessary dependencies:
npm install

<h3>Step 4: Set Up Environment Variables</h3>
Configure or modify the environment variables by creating or editing the .env file. This will set up the database and other required configurations for the web app.

<h3>Step 5: Create a Superuser</h3>
Create a superuser to access the backend portal using the following command:
medusa user -e admin@example.com -p password123

<h3>Step 6a: Run Redis Server (Optional)</h3>
If you have Redis installed, run the Redis server for caching purposes.
redis-server

<h3>Step 6b: Seed Data (Optional)</h3>
You can seed sample data into the database (optional but useful for testing).

<h3>Step 7: Run the Medusa Server</h3>
To start the Medusa server, run:
medusa develop
This will set up the Medusa backend server locally. You can now start building your commerce platform or modify the project as neede  d. 
<hr>
<h3>Output</h3>
The Medusa application launches a GUI on the port http://localhost:7001, which can be accessed using the superuser created earlier.

<h3>References</h3>
For more detailed information, visit the official Medusa documentation:
MedusaJS Local Development Guide

