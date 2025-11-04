pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/komma-gayathri/my-node-app.git'

            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Security Scan - Gitleaks') {
            steps {
                sh 'gitleaks detect --source . --no-git -v || true'
            }
        }

        stage('Security Scan - Trivy') {
            steps {
                sh 'trivy fs . || true'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    dockerImage = docker.build("my-node-app:${BUILD_NUMBER}")
                    echo "Docker image built successfully"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the app using Docker Compose...'
                // For real setup: sh 'docker-compose up -d'
            }
        }
    }
}
