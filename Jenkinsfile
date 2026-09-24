pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/youssef060902/Timesheet-DevOps.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t timesheet-devops-backend:latest .'
            }
        }
    }
}
