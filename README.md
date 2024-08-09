# Apache Airflow Deployment with Docker Compose

This project sets up Apache Airflow using Docker Compose, featuring a CeleryExecutor configuration with Postgres for the database backend and Redis as the message broker.

## Prerequisites

Before you start, make sure you have Docker and Docker Compose installed on your machine. Additionally, you need to have access to modify environment variables and volume paths as required for your environment.

## Components

The setup consists of the following services:

- **Airflow Webserver**: The web interface for Airflow.
  - **Port**: 8080
- **Airflow Scheduler**: Manages the scheduling of the jobs.
- **Airflow Worker**: Executes the tasks given by the scheduler.
- **Airflow Triggerer**: Handles the triggering of DAGs.
- **Redis**: Acts as the message broker for Celery.
  - **Exposed Port**: 6379 (not mapped to host)
- **Postgres**: Stores Airflow's metadata.
  - **Port**: 5432
- **Flower**: A web-based tool for monitoring and administrating Celery clusters.
  - **Port**: 5555
- **Airflow CLI**: Provides a CLI for Airflow.
- **Airflow Init**: Initializes the database and creates the necessary folders.

## Configuration

The `.env` file needs to be configured with the following environment variables:

- `AIRFLOW_IMAGE_NAME`: Set this to specify a custom Airflow image (default is `apache/airflow:2.5.1`).

Ensure the following default passwords and connections are changed for production deployments:

- Database connections in `AIRFLOW__DATABASE__SQL_ALCHEMY_CONN` and `AIRFLOW__CELERY__RESULT_BACKEND`.
- Redis connection in `AIRFLOW__CELERY__BROKER_URL`.
- Fernet Key in `AIRFLOW__CORE__FERNET_KEY` for encrypting sensitive data.

## Installation

1. **Clone the repository**:

   ```bash
   git clone [your-repository-url]
   cd [repository-name]
   ```

2. **Start the Service:

   ```bash
   docker-compose up -d
   ```

    This command will pull the necessary Docker images, and start the services defined in your docker-compose.yaml.

3. Check the logs:

    ```bash
    docker-compose logs -f
    ```

    Use this command to follow the logs of the services. It is helpful for debugging and ensuring all services are running correctly.

4. Visit Airflow Webserver:

    After the services are started, visit <http://localhost:8080> to access the Airflow web interface (airflow as default user and password).

5. Access Flower Dashboard:

    Flower can be accessed at <http://localhost:5555> to monitor the Celery workers.

## Data Persistence

The postgres-db-volume Docker volume is used to persist the PostgreSQL database data. Ensure that this volume is backed up regularly to avoid data loss.

## Stopping Services

To stop and remove all running services, use:

```bash
docker-compose down
```

## Conclusion

This setup provides a fully functional Airflow deployment suitable for development and production environments, depending on your security and customization needs.
