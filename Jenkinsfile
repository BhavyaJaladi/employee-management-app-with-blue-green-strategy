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
                echo "🏗 Building Backend using Maven"
                dir('backend') {
                    bat "${tool 'Maven-3.9.11'}/bin/mvn clean package -DskipTests"
                }
            }
        }

        stage('Frontend Build') {
            steps {
                echo "🌐 Building Frontend using Node"
                dir('frontend') {
                    bat "npm install"
                    bat "npm run build"
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'backend/target/*.jar'
                archiveArtifacts artifacts: 'frontend/dist/**'
            }
        }

        stage('Deploy (Simulated)') {
            steps {
                echo "Blue-Green Deployment skipped on Windows machine"
            }
        }
    }
}
