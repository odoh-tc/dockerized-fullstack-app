# Full-Stack FastAPI and React Template

Welcome to the Full-Stack FastAPI and React template repository. This repository serves as a demo application for interns, showcasing how to set up and run a full-stack application with a FastAPI backend and a ReactJS frontend using ChakraUI.

#### Here are the full requirements for completing this tasks:

Ensure the application runs locally before writing Dockerfiles
Configure the Frontend and Backend to listen on port 80
Obtain a domain name for the project
Write Dockerfiles to containerize the frontend and backend
Install adminer to enable database manager through its GUI
Configure Nginx proxy manager to handle reverse proxying and setup SSL certificates

## Project Structure

The repository is organized into two main directories:

- **frontend**: Contains the ReactJS application.
- **backend**: Contains the FastAPI application and PostgreSQL database integration.

Each directory has its own README file with detailed instructions specific to that part of the application.

## Getting Started

To get started with this template, please follow the instructions in the respective directories:

Clone the repository

```sh
 git clone url
 cd dockerized-fullstack-app
```

### backend

```sh
    cd backend
```

The backend depends on a postgresQL database, It would also require poetry to be installed before starting up.

1. Installing Poetry

```sh
    curl -sSL https://install.python-poetry.org | python3 -
```

Add Poetry to your PATH if it's not automatically added.

2. Install dependencies using Poetry:

```sh
    poetry install
```

3. Setup PostgreSQL:

```sh
    sudo apt update
    sudo apt install postgresql postgresql-contrib
    sudo -i -u postgres
    psql
    CREATE USER app WITH PASSWORD 'my_password';
    CREATE DATABASE app;
    \c app
    GRANT ALL PRIVILEGES ON DATABASE app TO app;
    GRANT ALL PRIVILEGES ON SCHEMA public TO app;
    \q
    exit
```

4. Set database credentials

```sh
    POSTGRES_SERVER=localhost
    POSTGRES_PORT=5432
    POSTGRES_DB=app
    POSTGRES_USER=app
    POSTGRES_PASSWORD=my_password
```

5. Set up the database with the necessary tables:

```sh
    poetry run bash ./prestart.sh
```

6. Run the backend server

```sh
    poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

### frontend

```sh
    cd backend
```

1. The frontend was built with Nodejs and npm for dependency management.

```sh
    sudo apt update
    sudo apt install nodejs npm
```

2. Install dependencies:

```sh
    npm install
```

3.  The login credentials can be found in the .env located in the backend folder

```sh
    FIRST_SUPERUSER=devops@hng.tech
    FIRST_SUPERUSER_PASSWORD=devops#HNG11
```

3.  To properly route the browser to the remote server running the application. we will have to Change the VITE_API_URL variable in the frontend .env file:

```sh
    VITE_API_URL=http://<your_server_IP>:8000
```

3. we need to tell our backend to accept request coming from that particular IP address. In our backed .env file we need to add http://<your_server_IP>:5173 to the end of the string of allowed IPs

```sh
    BACKEND_CORS_ORIGINS="http://localhost,http://localhost:5173,https://localhost,https://localhost:5173,http://<your_server_IP>:5173"
```

3. Run the fronted server

```sh
    npm run dev -- --host
```

4. Accessing the application

```sh
    http://<your_server_IP>:5173
    curl localhost:5173
```

## Deployment with Docker-compose

- Add the Dockerfile to both frontend and backend with docker-compose in root directory

```sh
    docker-compose up -d
```
