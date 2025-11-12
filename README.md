# S&P 500 Intraday Data Pipeline 

An automated ETL pipeline that extracts, transforms, and loads real-time intraday data for the S&P 500 using Apache Airflow running in Docker.

The pipeline fetches 1-minute interval stock data from Yahoo Finance, processes it for analytics, and loads it into Amazon S3 and Snowflake for storage and visualization.


## Project Overview

This project uses Apache Airflow to orchestrate an ETL pipeline for real-time S&P 500 data.

Workflow Summary:

Extract: Pulls 1-minute interval data for the top 10 S&P 500 tickers using yfinance.

Transform: Adds minute returns, trading hours, and other metrics.

Load: Uploads cleaned data to Amazon S3 and Snowflake for long-term storage and analysis.

All tasks run in Dockerized Airflow containers, ensuring a reproducible and isolated environment.

## Technologies Used

Apache Airflow	Workflow orchestration and scheduling

Docker / Docker Compose	Containerization and environment management

yfinance	Fetching real-time market data

pandas	Data cleaning and transformation

Amazon S3	Cloud data storage

Snowflake	Data warehousing and analytics

Python 3.x	Primary programming language

### Prerequisites

Before setup, make sure you have:

Docker & Docker Compose — Install Docker

Python 3.x installed

AWS Account — S3 credentials for storage

Snowflake Account — Database and warehouse access

Git for cloning the repository

## Setup
### Docker Setup


Build and start services:

sudo docker-compose up --build -d


Access Airflow UI: http://localhost:8080

Login Credentials:

Username: airflow
Password: airflow

### Airflow Setup

Initialize Airflow database:

sudo docker-compose run --rm airflow-init


Configure connections in Airflow UI:

AWS S3 Connection: Conn ID aws_default — Access Key & Secret Key

Snowflake Connection: Conn ID snowflake_default — Account, User, Password, Database, Schema, Warehouse

Schedule the ETL DAG
Runs automatically based on your configured schedule (@daily or custom).

## Usage
### Automation

Pipeline executes automatically based on your schedule.

All tasks (Extract → Transform → Load) are fully traceable in Airflow.

### Monitoring

Use the Airflow UI (http://localhost:8080
) to:

Track task success/failure 

View real-time logs 

Trigger manual DAG runs 

## Data Outputs

### Amazon S3:

s3://your-bucket/sp500_intraday/{trading_date}.csv


Partitioned by trading date for efficient querying.

### Snowflake:

Data loaded into:

DATABASE.SP500_SCHEMA.INTRADAY_DATA


Ready for BI tools (Tableau, Power BI) and SQL analytics.

