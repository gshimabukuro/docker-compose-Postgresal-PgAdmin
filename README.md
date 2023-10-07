I apologize for missing the network creation part. Here's the updated README.md with the network creation command included:

```markdown
# Docker Compose Configuration for PostgreSQL, pgAdmin, and Redis

This Docker Compose configuration file sets up containers for PostgreSQL, pgAdmin, and Redis. It allows you to easily manage and run these services for your development or testing environment.

## Prerequisites
Before you begin, ensure that you have Docker and Docker Compose installed on your system.

## Usage
1. Clone or download this repository to your local machine.

2. Navigate to the directory containing this `README.md` file and the `docker-compose.yml` file.

3. Create a file named `database.env` in the same directory. Add your PostgreSQL environment variables to this file. Here's an example `database.env` file:

   ```ini
   POSTGRES_DB=mydatabase
   POSTGRES_USER=myuser
   POSTGRES_PASSWORD=mypassword
   ```

4. Customize the container names, image versions, environment variables, and volumes in the `docker-compose.yml` file to suit your requirements.

5. Run the following command to create the external network:

   ```bash
   docker network create \
       --driver bridge \
       --subnet 172.18.0.0/16 \
       --gateway 172.18.0.1 \
       docker-compose-postgresal-pgadmin_mynetwork
   ```

   This will create an external network named `docker-compose-postgresal-pgadmin_mynetwork` with the specified subnet and gateway.

6. Run the following command to start the containers:

   ```bash
   docker-compose up -d
   ```

   This will launch the PostgreSQL, pgAdmin, and Redis containers in the background.

7. Access pgAdmin in your web browser by navigating to `http://localhost:5050`. Log in using the following credentials:

   - **Email:** admin@admin.com
   - **Password:** admin

8. In pgAdmin, you can add a new PostgreSQL server with the following details:

   - **Host name/address:** db
   - **Port:** 5432
   - **Username:** (Use the PostgreSQL username from your `database.env` file)
   - **Password:** (Use the PostgreSQL password from your `database.env` file)

9. You can also connect to the Redis container using the hostname `redis` and port `6379`.

10. To stop and remove the containers, run:

    ```bash
    docker-compose down
    ```

## Container Information
### PostgreSQL (postgres_container)
- Container Name: postgres_container
- Image: postgres:16.0
- Restart Policy: always
- Environment Variables: Loaded from `database.env`
- Ports:
  - Host: 5432
  - Container: 5432
- Volume Mount: D:\\database\\postgresql\\postgres_data:/var/lib/postgresql/data
- Network Configuration:
  - IPv4 Address: 172.18.0.10 (Choose an available IP address within the subnet)

### pgAdmin (pgadmin4_container)
- Container Name: pgadmin4_container
- Image: dpage/pgadmin4:7.7
- Restart Policy: always
- Environment Variables:
  - PGADMIN_DEFAULT_EMAIL=admin@admin.com
  - PGADMIN_DEFAULT_PASSWORD=admin
- Ports:
  - Host: 5050
  - Container: 80
- Volume Mount: D:\\database\\postgresql\\pgadmin_data:/var/lib/pgadmin
- Network Configuration:
  - IPv4 Address: 172.18.0.11 (Choose an available IP address within the subnet)

### Redis (redis_container) [Optional]
- Image: redis:latest
- Container Name: redis_container
- Restart Policy: always
- Ports:
  - Host: 6379
  - Container: 6379
- Volume Mount: D:\\database\\redis_data:/data
- Network Configuration:
  - IPv4 Address: 172.18.0.12 (Choose an available IP address within the subnet)

## Network Configuration
The containers are connected to an external Docker network named `docker-compose-postgresal-pgadmin_mynetwork`. You can use this network to facilitate communication between containers if needed.

Feel free to modify this Docker Compose configuration to suit your specific project requirements. Enjoy using PostgreSQL, pgAdmin, and Redis in Docker containers for your development needs!
```

This includes the network creation command and updates the README.md accordingly.