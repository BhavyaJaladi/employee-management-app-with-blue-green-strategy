pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/siddarthapeddi/employee-management-app-with-blue-green-strategy.git',
                        credentialsId: '5cc29cec-fb86-42dd-840b-d6b76b053f81'
                    ]]
                ])
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
                echo "Docker build requires Linux — skipping on Windows."
            }
        }

        stage('Blue-Green Deployment (Simulated)') {
            steps {
                echo "Blue-Green deploy disabled — requires Linux + Docker Swarm."
            }
        }
    }
}
