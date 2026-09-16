# Project Documentation

## 1. Project Overview

This project demonstrates an end-to-end DevOps workflow for deploying and monitoring a containerized web application on AWS.

The project combines Infrastructure as Code, configuration management, containerization, Kubernetes orchestration, CI/CD, ingress networking, and monitoring.

## 2. Infrastructure

Terraform was used to provision the AWS infrastructure.

### AWS Resources

- VPC
- Internet Gateway
- Public Subnets
- Route Table
- Security Groups
- IAM Roles
- Amazon EKS Cluster
- EKS Managed Node Group
- EC2 instance for Ansible
- Amazon ECR repository

## 3. Configuration Management

Ansible was used to configure the EC2 web server.

The Ansible implementation uses:

- Roles
- Jinja2 templates
- Variables
- Handlers
- Nginx

The server is configured automatically through the Ansible playbook.

## 4. Containerization

The application is packaged using Docker.

The Docker image uses Nginx as the base image and serves the application from the container.

The image is stored in Amazon ECR.

## 5. Kubernetes Deployment

The application is deployed to Amazon EKS.

Kubernetes resources include:

- Deployment
- Service
- Ingress

The Deployment runs multiple application replicas.

The Service provides internal access to the application pods.

## 6. Ingress and Load Balancing

The AWS Load Balancer Controller is used to integrate Kubernetes Ingress with AWS.

The application traffic follows this path:

Client
→ AWS Application Load Balancer
→ Kubernetes Ingress
→ Kubernetes Service
→ Application Pods

## 7. CI/CD

GitHub Actions automates the deployment workflow.

The production workflow contains four sequential jobs:

### Terraform

Terraform initializes the infrastructure configuration and performs a Terraform plan.

### Docker

The application image is built and pushed to Amazon ECR.

### Ansible

The Ansible playbook configures the web server.

### Kubernetes

The Kubernetes configuration is applied to the EKS cluster and the deployment is verified.

## 8. Monitoring

The Kubernetes environment is monitored using Prometheus and Grafana.

The monitoring stack includes:

- Prometheus
- Grafana
- kube-state-metrics
- Node Exporter

The Grafana dashboard includes:

- Node CPU Usage
- Node Memory Usage
- Kubernetes Pod Count

## 9. Security

GitHub Actions authenticates with AWS using GitHub OIDC instead of storing long-lived AWS access keys inside GitHub.

Kubernetes access for the CI/CD workflow is provided through an EKS access entry.

Sensitive local configuration such as the Ansible inventory is excluded from Git using `.gitignore`.

## 10. Verification

The production workflow was successfully executed through GitHub Actions.

The following stages completed successfully:

- Terraform Plan
- Docker Build and Push
- Ansible Deployment
- Kubernetes Deployment

The deployed application was successfully accessed through the AWS Application Load Balancer.

Prometheus metrics were verified and Grafana successfully queried Prometheus as its monitoring data source.

## 11. Skills Demonstrated

This project demonstrates practical experience with:

- Linux
- Git
- GitHub
- GitHub Actions
- AWS
- IAM
- OIDC
- Terraform
- Ansible
- Docker
- Amazon ECR
- Amazon EKS
- Kubernetes
- Ingress
- AWS Load Balancer Controller
- Prometheus
- Grafana
- CI/CD
- Infrastructure as Code
- Configuration Management
- Monitoring
