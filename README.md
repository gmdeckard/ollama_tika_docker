# Ollama and Apache Tika Docker Compose

This repository contains a Docker Compose setup for running an Ollama server and an Apache Tika server.

## Services

- **Ollama**: A service running the Ollama application.
- **Apache Tika**: A service running the Apache Tika server for document text extraction.

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

  tika:
    image: apache/tika:latest
    container_name: tika
    ports:
      - "9998:9998"
    restart: always

volumes:
  ollama_data:
