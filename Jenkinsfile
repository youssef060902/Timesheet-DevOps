```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/youssef060902/Timesheet-DevOps.git'
            }
        }

        stage('Test + JaCoCo') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=timesheet-devops \
                        -Dsonar.projectName=Timesheet-DevOps \
                        -Dsonar.host.url=http://localhost:9000
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t timesheet-devops-backend:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin

                        docker tag timesheet-devops-backend:latest \
                        $DOCKER_USERNAME/timesheet-devops-backend:latest

                        docker push \
                        $DOCKER_USERNAME/timesheet-devops-backend:latest

                        docker logout
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker compose pull
                    docker compose up -d
                '''
            }
        }
    }
}
```

