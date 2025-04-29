pipeline {
    agent any

    environment {
        EMAIL = 'paduchuridinesh15218@gmail.com'  // Replace with your actual email
    }

    stages {
        stage('Disable SSL Verify') {
            steps {
                bat 'git config --global http.sslVerify false'
            }
        }
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

    post {
        success {
            mail to: "${EMAIL}",
                 subject: "✅ Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build was successful!\n\nProject: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nURL: ${env.BUILD_URL}"
        }

        failure {
            mail to: "${EMAIL}",
                 subject: "❌ Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed.\n\nProject: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nURL: ${env.BUILD_URL}"
        }
    }
}
