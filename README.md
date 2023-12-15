# Deploying a Flask API and MySQL Server on Kubernetes

This repository contains code to deploy a MySQL server on a Kubernetes cluster, attach a persistent volume for data persistence, and deploy a Flask API for managing users in the MySQL database.

## Prerequisites

Ensure you have the following installed:
- Docker
- Kubernetes CLI (kubectl)
- Minikube (https://kubernetes.io/docs/tasks/tools/)

## Getting Started

1. **Clone the repository.**

    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. **Configure Docker to use the Docker daemon in your Kubernetes cluster.**

    ```bash
    eval $(minikube docker-env)
    ```

3. **Pull the latest MySQL image from Dockerhub.**

    ```bash
    docker pull mysql
    ```

4. **Build a Kubernetes API image with the Dockerfile in this repo.**

    ```bash
    docker build . -t flask-api
    ```

## Secrets

Kubernetes Secrets are used to store sensitive information. Follow these steps to set up a password for the MySQL root user:

1. **Encode your password in the terminal.**

    ```bash
    echo -n super-secret-password | base64
    ```

2. **Add the output to the `flaskapi-secrets.yml` file at the `db_root_password` field.**

## Deployments

1. **Add the secrets to your Kubernetes cluster.**

    ```bash
    kubectl apply -f flaskapi-secrets.yml
    ```

2. **Create the persistent volume and persistent volume claim for the database.**

    ```bash
    kubectl apply -f mysql-pv.yml
    ```

3. **Create the MySQL deployment.**

    ```bash
    kubectl apply -f mysql-deployment.yml
    ```

4. **Create the Flask API deployment.**

    ```bash
    kubectl apply -f flaskapp-deployment.yml
    ```

Check the status of the pods, services, and deployments.

## Creating Database and Schema

Connect to the MySQL database to set up the database and table using the following commands:

```bash
kubectl run -it --rm --image=mysql --restart=Never mysql-client -- mysql --host mysql --password=<super-secret-password>
