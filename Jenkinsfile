pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Akhila-Gardas/Java-App.git'
            }
        }

        stage('Build Java Application') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t java-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    docker stop java-app-container || true
                    docker rm java-app-container || true
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                    docker run -d \
                    --name java-app-container \
                    -p 8080:8080 \
                    java-app
                '''
            }
        }

        stage('Check Container') {
            steps {
                sh 'docker ps'
            }
        }

    }
}