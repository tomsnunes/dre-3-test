# Changelog

## Fixed

### compose.yaml

- Changed the DAG folder name from "dag" to "dags" to correctly mount the volume at "/opt/airflow/dags" (line 14).
- Updated the POSTGRES_USER environment variable from "admin" to "airflow" to meet expected configuration (line 31).
- Corrected the Airflow webserver health check port from an incorrect placeholder to 8080 (line 59).

### smooth.py

- Renamed the schedule parameter to schedule_interval to align with the expected argument name in Airflow (line 7).
- Assigned the output of the smooth() function to smooth_dag to ensure the DAG is properly registered with Airflow (line 16).
