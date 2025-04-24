pipeline {
    agent any

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
        stage('Clean Up Old Container') {
            steps {
                bat 'docker stop box-office-deploy-web-1 || exit 0'
                bat 'docker rm box-office-deploy-web-1 || exit 0'
            }
        }
        stage('Clean Up Old Image') {
            steps {
                bat 'docker rmi boxoffice-app || exit 0'
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
            emailext(
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Build Successful!</p>
                     <p><b>Project:</b> ${env.JOB_NAME}</p>
                     <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                     <p><b>URL:</b> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                to: 'paduchuridinesh15218@gmail.com',
                mimeType: 'text/html'
            )
        }
        failure {
            emailext(
                subject: "❌ FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Build Failed!</p>
                     <p><b>Project:</b> ${env.JOB_NAME}</p>
                     <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                     <p><b>URL:</b> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
                to: 'paduchuridinesh15218@gmail.com',
                mimeType: 'text/html'
            )
        }
    }
}
