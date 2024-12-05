# **Setup Instructions for Dockerized Laravel Application**

This guide will walk you through the steps to get your Laravel project running in Docker, including building images, running containers, executing Laravel commands, and accessing the containers via shell.

---

## Step 1: Copy `.env.example` to `.env`

Before starting your Docker containers, you need to set up your environment configuration by copying the `.env.example` file to `.env`.

```bash
cp .env.example .env
```

This will create the `.env` file, where Laravel will look for environment variables.

---

## Step 2: Build Docker Images

Build the Docker images using Docker Compose. This step will read your `docker-compose.yml` file and build the necessary images for the application, web server, and database.

```bash
docker-compose build
```

This will create the containers for your Laravel application (`app`), the database (`db`), and the web server (`nginx`).

---

## Step 3: Make the Scripts Executable

You have three scripts to control the Docker containers:

- **docker/start** - Start the containers
- **docker/stop** - Stop the containers
- **docker/bash** - Access the application container shell

Before using these scripts, you need to make them executable. Run the following commands:

```bash
chmod +x docker/start
chmod +x docker/stop
chmod +x docker/bash
```

This will allow you to run the scripts directly from the command line.

---

## Step 4: Start the Docker Containers

Now that the scripts are executable, you can start the containers by running the `start` script.

```bash
./docker/start
```

Alternatively, if you want to use Docker Compose directly, you can start the containers in detached mode with:

```bash
docker-compose up -d
```

This will start the application, web server, and database containers in the background.

---

## Step 5: Access the Application Container's Shell

To execute commands inside the application container, you can open an interactive bash shell using the `docker/bash` script. This allows you to run Laravel commands and interact with the container.

```bash
./docker/bash
```

Alternatively, you can manually access the container's shell with:

```bash
docker exec -it laravel-app bash
```

This will give you a shell prompt inside the container where you can execute Laravel commands.

---

## Step 6: Generate Laravel Application Key

Now that you're inside the container, generate the application key for your Laravel project. This key is required for encryption and security purposes.

```bash
php artisan key:generate
```

This will set the `APP_KEY` in the `.env` file.

---

## Step 7: Run Database Migrations

Next, run the database migrations to create the necessary tables in your MySQL database.

```bash
php artisan migrate
```

This will apply all the database migrations defined in your Laravel application.

---

## Step 8: Seed the Database (Optional)

If your Laravel project comes with some predefined data (like user roles or sample data), you can seed the database with:

```bash
php artisan db:seed
```

This step is optional but recommended if you want to populate the database with initial data.

---

## Step 9: Access the Application in Browser

Once everything is set up, you can access your Laravel application in the browser. The application will be served by Nginx at port 80.

Visit the following URL in your browser:

```
http://localhost:80
```

---

## Step 10: Stop the Docker Containers

When you're done working with the application, you can stop the containers using the `docker/stop` script:

```bash
./docker/stop
```

Alternatively, you can stop and remove all containers manually with:

```bash
docker-compose down
```

This will stop and remove all running containers.