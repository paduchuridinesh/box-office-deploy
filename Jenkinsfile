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
                sh 'docker build -t boxoffice-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
