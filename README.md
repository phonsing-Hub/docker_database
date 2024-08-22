# Docker Compose Setup

This `docker-compose.yml` file sets up a multi-container environment with PostgreSQL, pgAdmin, MySQL, phpMyAdmin, MongoDB, and Mongo Express. Each service is configured to run in its own container and communicate over a shared Docker network.

## Services

### PostgreSQL

- **Container Name**: `postgres`
- **Image**: `arm64v8/postgres`
- **Environment Variables**:
  - `POSTGRES_USER`: The username for the PostgreSQL superuser.
  - `POSTGRES_PASSWORD`: The password for the PostgreSQL superuser.
  - `PGDATA`: The directory where PostgreSQL will store its data.
- **Volumes**:
  - `postgres:/data/postgres`: Stores PostgreSQL data.
- **Ports**:
  - `5432:5432`: Exposes PostgreSQL on port 5432.
- **Network**: `database_network`
- **Restart Policy**: `unless-stopped`

### pgAdmin

- **Container Name**: `pgadmin`
- **Image**: `dpage/pgadmin4`
- **Environment Variables**:
  - `PGADMIN_DEFAULT_EMAIL`: Email used to log into pgAdmin.
  - `PGADMIN_DEFAULT_PASSWORD`: Password used to log into pgAdmin.
  - `PGADMIN_CONFIG_SERVER_MODE`: Configures pgAdmin in desktop mode.
- **Volumes**:
  - `pgadmin:/var/lib/pgadmin`: Stores pgAdmin settings and metadata.
- **Ports**:
  - `8081:80`: Exposes pgAdmin on port 8081.
- **Network**: `database_network`
- **Restart Policy**: `unless-stopped`

### MySQL

- **Container Name**: `mysql`
- **Image**: `arm64v8/mysql`
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`: The root password for MySQL.
  - `MYSQL_DATABASE`: The name of the initial database created.
- **Volumes**:
  - `mysql_data:/var/lib/mysql`: Stores MySQL data.
- **Ports**:
  - `3306:3306`: Exposes MySQL on port 3306.
- **Network**: `database_network`
- **Restart Policy**: `unless-stopped`

### phpMyAdmin

- **Container Name**: `phpmyadmin`
- **Image**: `arm64v8/phpmyadmin`
- **Environment Variables**:
  - `PMA_HOST`: The hostname of the MySQL service.
  - `MYSQL_ROOT_PASSWORD`: The root password for MySQL.
- **Ports**:
  - `8080:80`: Exposes phpMyAdmin on port 8080.
- **Network**: `database_network`
- **Restart Policy**: `unless-stopped`

### MongoDB

- **Container Name**: `mongodb`
- **Image**: `arm64v8/mongo`
- **Environment Variables**:
  - `MONGO_INITDB_ROOT_USERNAME`: The root username for MongoDB.
  - `MONGO_INITDB_ROOT_PASSWORD`: The root password for MongoDB.
- **Volumes**:
  - `mongodb_data:/data/db`: Stores MongoDB data.
- **Ports**:
  - `27017:27017`: Exposes MongoDB on port 27017.
- **Network**: `database_network`
- **Restart Policy**: `unless-stopped`

## Networks

- **`database_network`**: A bridge network allowing communication between containers.

## Volumes

- **`postgres`**: Volume for PostgreSQL data.
- **`pgadmin`**: Volume for pgAdmin settings and metadata.
- **`mysql_data`**: Volume for MySQL data.
- **`mongodb_data`**: Volume for MongoDB data.

## Access

- **pgAdmin**: [http://localhost:8081](http://localhost:8081)
- **phpMyAdmin**: [http://localhost:8080](http://localhost:8080)

## Usage

To start all services, run:
```bash
docker-compose up -d
