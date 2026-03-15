# YouTube API ELT Pipeline

A project to practice implementing a complete ELT pipeline.

It uses Python, Docker, PostgreSQL, and Apache Airflow, testing and CI/CD.

## Dataset

The dataset comes from the **YouTube Data API**, using videos from the **Computerphile** channel as an example.

## Project Overview

This project implements an ELT pipeline orchestrated with Apache Airflow running inside Docker containers. Airflow defines workflows as DAGs, where tasks represent steps in a pipeline and dependencies determine execution order.

The pipeline works as follows:

1. **Extract**  
   Python scripts call the YouTube API to retrieve video metadata.

2. **Load**  
   Raw data is stored in a PostgreSQL staging schema.

3. **Transform**  
   Python transformations clean the data and load it into a core schema for analytics.

**Containerization using :**

- Docker  
- Docker Compose  

**Orchestration using :**

- Apache Airflow  

**Data Storage using :**

- PostgreSQL  

**Testing using :**

- pytest  
- Soda Core  

**CI/CD using :**

- GitHub Actions

## Containerization

Airflow runs inside Docker using the docker-compose setup provided by the Airflow project. A custom Docker image extends the Airflow base image to install additional Python dependencies required for the project.

This image is automatically:

1. Built through GitHub Actions**
2. Pushed to Docker Hub
3. Used by docker-compose to run the Airflow services.

Environment variables are used for:

- Airflow connections  
- Airflow variables  
- database credentials  

A Fernet key is configured to encrypt sensitive information stored in Airflow.

## Airflow DAGs

The pipeline is orchestrated through three DAGs:

### produce_json

Extracts data from the YouTube API and generates a JSON file containing the raw data.

### update_db

Processes the JSON file and loads the data into the staging and core PostgreSQL schemas.

### data_quality

Runs data quality checks on the database using Soda.


---

This project has been conceived following the original code found on this repository :

https://github.com/MattTheDataEngineer/YT_ELT

