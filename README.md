# Ollama, Apache Tika, PostgreSQL, and Ubuntu Jammy Docker Compose

This repository contains a Docker Compose setup for running an Ollama server, an Apache Tika server, a PostgreSQL database server, and an Ubuntu Jammy server.

## Services

- **Ollama**: A service running the Ollama application.
- **Apache Tika**: A service running the Apache Tika server for document text extraction.
- **PostgreSQL**: A service running the PostgreSQL database server.
- **Ubuntu Jammy**: A service running Ubuntu Jammy.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

To get the services up and running, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/gmdeckard/ollama_tika_docker.git
    cd ollama_tika_docker
    ```

2. Start the services using Docker Compose:
    ```bash
    docker-compose up -d
    ```

3. Verify that the services are running:
    - Ollama: [http://localhost:8000](http://localhost:8000)
    - Apache Tika: [http://localhost:9998](http://localhost:9998)
    - PostgreSQL: Accessible on port 5432
    - Ubuntu Jammy: Running as a service

## Docker Compose File

Below is the `docker-compose.yml` file used to set up the services:

```yaml
version: '3.8'

services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama
    ports:
      - "8000:8000"
    environment:
      - OLLAMA_ENV=production
    volumes:
      - ollama_data:/data
    restart: always

  ubuntu:
    image: ubuntu:jammy
    container_name: ubuntu_jammy
    restart: always

  db:
    image: postgres:latest
    container_name: postgres_db
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=yourdatabase
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: always

  tika:
    image: apache/tika:latest
    container_name: tika
    ports:
      - "9998:9998"
    restart: always

volumes:
  ollama_data:
  postgres_data:
