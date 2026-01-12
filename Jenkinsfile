pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/sanjay6747/java-web-app.git'
            }
        }

        stage('Build Java Web App') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t java-web-app:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f java-web-app || true
                docker run -d -p 8080:8080 \
                --name java-web-app \
                java-web-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}
