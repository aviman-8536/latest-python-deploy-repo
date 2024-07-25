pipeline {
    agent any
    environment {
        GIT_URL = 'https://github.com/aviman-8536/latest-python-deploy-repo.git'
        GIT_BRANCH = 'dev'
        GIT_CREDENTIALS = 'github_credentials' // Make sure this credential ID exists in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git url: env.GIT_URL, branch: env.GIT_BRANCH, credentialsId: env.GIT_CREDENTIALS
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("myapppython")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    dockerImage.run('-d --avi')
                }
            }
        }
        stage('Show Results') {
            steps {
                script {
                    sh 'docker logs avi'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker stop avi'
                sh 'docker rm avi'
            }
        }
    }
}