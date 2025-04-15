pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/paduchuridinesh/box-office-deploy.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t boxoffice-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                bat 'docker-compose up -d'
            }
        }
    }
}
