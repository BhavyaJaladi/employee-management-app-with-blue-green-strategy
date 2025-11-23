pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
        nodejs 'Node-24'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/siddarthapeddi/employee-management-app-with-blue-green-strategy.git',
                        credentialsId: 'github-pat'
                    ]]
                ])
            }
        }

        stage('Backend Build') {
            steps {
                echo "🔧 Building Backend with Maven"
                dir('backend') {
                    bat 'mvn -version'
                    bat 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Frontend Build') {
            steps {
                echo "🌐 Building Frontend"
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

        stage('Docker Build (Skipped)') {
            when { expression { false } }
            steps {
                echo "🐳 Docker skipped on Windows"
            }
        }

        stage('Blue-Green Deployment (Simulated)') {
            steps {
                echo "🔵🟢 Blue-Green deploy skipped"
            }
        }
    }
}
