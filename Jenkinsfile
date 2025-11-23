pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: url: 'https://github.com/siddhartha-peddi/employee-management-app-with-blue-green-strategy.git'

            }
        }

        stage('Backend Build') {
            steps {
                dir('backend') {
                    bat 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Frontend Build') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
                archiveArtifacts artifacts: 'frontend/dist/**', fingerprint: true
            }
        }

        stage('Docker Build (Optional)') {
            when {
                expression { return fileExists('docker/Dockerfile') }
            }
            steps {
                echo "Docker build disabled on Windows Jenkins. Use Linux agent for real builds."
            }
        }

        stage('Blue-Green Deployment (Simulated)') {
            steps {
                echo "Blue-Green deploy disabled on Windows. Requires Linux + bash."
            }
        }
    }
}

