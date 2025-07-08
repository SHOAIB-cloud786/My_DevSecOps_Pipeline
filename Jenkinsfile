pipeline {
    agent any
    environment {
        IMAGE_NAME = "nodejs-app:${BUILD_NUMBER}"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/someuser/sample-nodejs-app.git'
            }
        }
        stage('SonarQube - SAST') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Trivy Scan') {
            steps {
                sh 'trivy image $IMAGE_NAME || true'
            }
        }
        stage('Terraform Apply') {
            steps {
                dir('infra') {
                    sh 'terraform init && terraform apply -auto-approve'
                }
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
        stage('DAST Scan - OWASP ZAP') {
            steps {
                sh 'zap-cli quick-scan --self-contained http://your-app-url'
            }
        }
    }
}