# SecureCloud – DevSecOps CI/CD Project (Shoaib Khan)

This project demonstrates a secure DevSecOps CI/CD pipeline for a sample Node.js web application deployed on AWS using Kubernetes (EKS), Jenkins, Terraform, and various security tools.

## Tech Stack & Tools
- Jenkins for CI/CD
- Docker & Kubernetes (EKS)
- Terraform for IaC
- SonarQube (SAST)
- Trivy (Container Scanning)
- OWASP ZAP (DAST)
- HashiCorp Vault (Secrets)
- Prometheus & Grafana (Monitoring)

## Pipeline Overview
1. Code pushed to GitHub triggers Jenkins pipeline.
2. Jenkins builds Docker image.
3. Runs SonarQube for static code analysis (SAST).
4. Scans Docker image using Trivy.
5. Deploys infrastructure with Terraform.
6. Deploys app to EKS using kubectl.
7. Performs DAST scan using OWASP ZAP.
8. Sends alerts/logs to ELK/Grafana.
