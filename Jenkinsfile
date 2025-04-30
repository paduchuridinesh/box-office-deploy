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
        mail to: "${EMAIL}",
             subject: "✅ Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
             body: """Hello Dinesh,

    The Jenkins build completed successfully.

    Details:
    - Project: ${env.JOB_NAME}
    - Build Number: ${env.BUILD_NUMBER}
    - Status: SUCCESS
    - Branch: ${env.GIT_BRANCH}
    - Git Commit: ${env.GIT_COMMIT}
    - Build URL: ${env.BUILD_URL}

    Regards,
    Jenkins
    """
        }

    failure {
        mail to: "${EMAIL}",
             subject: "❌ Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
             body: """Hello Dinesh,

    The Jenkins build has failed.

    Details:
    - Project: ${env.JOB_NAME}
    - Build Number: ${env.BUILD_NUMBER}
    - Status: FAILURE
    - Branch: ${env.GIT_BRANCH}
    - Git Commit: ${env.GIT_COMMIT}
    - Build URL: ${env.BUILD_URL}

    Please check the Jenkins console log for more details.

    Regards,
    Jenkins
    """
        }
    }
}
