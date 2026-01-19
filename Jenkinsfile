pipeline {
    agent any

    environment {
        IMAGE_NAME = "gauravmcc/jenkins-docker-demo"
        IMAGE_TAG = "latest"
        DOCKERHUB = credentials('dockerhub-creds')
    }

    stages {

        stage('Verify Docker Installation') {
            steps {
                bat 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat """
                docker build -t %IMAGE_NAME%:%IMAGE_TAG% .
                """
            }
        }

        stage('Login to Docker Hub') {
            steps {
                bat """
                echo %DOCKERHUB_PSW% | docker login -u %DOCKERHUB_USR% --password-stdin
                """
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                bat """
                docker push %IMAGE_NAME%:%IMAGE_TAG%
                """
            }
        }
    }

    post {
        success {
            echo "SUCCESS: Docker image gauravmcc/jenkins-docker-demo pushed to Docker Hub!"
        }
        failure {
            echo "ERROR: Pipeline failed. Check Jenkins console logs."
        }
    }
}
