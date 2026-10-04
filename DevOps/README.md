# Terraform + Docker Infrastructure Demo

A small infrastructure automation project demonstrating how Terraform can be used to manage a Docker container and automate the Docker image build process.

## Overview

This project uses **Terraform** to provision and manage a Docker container running a lightweight Nginx web server.

A PowerShell script is used to build the Docker image, while Terraform manages the resulting Docker image and container.

### Architecture

```text
buildImg.ps1
      │
      │ docker build
      ▼
Docker Image
my-nginx-image
      │
      │ Terraform manages
      ▼
Docker Container
my-nginx-container
      │
      ▼
Nginx Web Server
      │
      │ port 80
      ▼
localhost:80
```

## Technologies

* Terraform 1.10+
* Docker
* Docker Provider for Terraform
* PowerShell
* Nginx
* HCL

## What I Implemented

* Defined Docker infrastructure using Terraform
* Automated Docker image building with PowerShell
* Managed Docker image and container resources through Terraform
* Configured resource dependencies to ensure the image build completes before the container is created
* Configured Docker container port mapping
* Packaged web content into an Nginx-based Docker image

## Project Structure

```text
.
├── main.tf
├── buildImg.ps1
├── Dockerfile
├── index.html
├── .gitignore
├── .terraform.lock.hcl
└── README.md
```

## Prerequisites

Before running the project, make sure the following are installed:

* Docker Desktop
* Terraform
* PowerShell

Docker Desktop must be running before executing Terraform commands.

## Getting Started

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd terraform-docker-demo
```

### 2. Initialize Terraform

```bash
terraform init
```

### 3. Review the execution plan

```bash
terraform plan
```

### 4. Create the infrastructure

```bash
terraform apply
```

Confirm the operation when prompted.

Terraform will:

1. Execute the PowerShell build script
2. Build the Docker image
3. Create the Docker container
4. Map host port `80` to container port `80`

During the image build process, the PowerShell script will report whether the Docker image was built successfully.

### 5. Verify the container

Open:

```text
http://localhost
```

The Nginx container should serve the contents of `index.html`.

### 6. Destroy the infrastructure

When finished:

```bash
terraform destroy
```

This removes the Docker container managed by Terraform.

## Key Concepts Demonstrated

### Infrastructure as Code

Terraform is used to define infrastructure declaratively rather than manually creating Docker resources.

### Resource Dependencies

The Docker image resource depends on the image build step:

```hcl
depends_on = [null_resource.build_image]
```

This ensures the image build process is completed before Terraform proceeds with the dependent resources.

### Containerization

The web content is packaged into a Docker image based on Nginx and executed as an isolated container.

### Infrastructure Lifecycle

Terraform provides a consistent workflow for creating, reviewing, and destroying the infrastructure:

```text
terraform init
       ↓
terraform plan
       ↓
terraform apply
       ↓
terraform destroy
```

## Notes

This is a learning/demo project created to practice infrastructure automation, containerization, and Infrastructure as Code concepts using Terraform and Docker.
