pipeline {
    agent any
    environment {
        GIT_URL = 'https://github.com/aviman-8536/python-deploy-now.git'
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
                    dockerImage.run('-d --name your-container-name')
                }
            }
        }
        stage('Show Results') {
            steps {
                script {
                    sh 'docker logs your-container-name'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker stop your-container-name'
                sh 'docker rm your-container-name'
            }
        }
    }
}