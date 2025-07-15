pipeline {
    agent any

    environment {
        REGISTRY = "joerozen"                       // this is your Docker Hub username
        REGISTRY_URL = "https://index.docker.io/v1/"
        IMAGE_NAME = "my-docker-app-jenkins-1"
        TAG = "latest"
        CREDENTIALS_ID = "dockerhub-creds"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Debug Branch') {
            steps {
                echo "Branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${REGISTRY}/${IMAGE_NAME}:${TAG} ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: env.CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo "$DOCKER_PASS" | docker login ${REGISTRY_URL} -u "$DOCKER_USER" --password-stdin
                        docker push ${REGISTRY}/${IMAGE_NAME}:${TAG}
                        docker logout ${REGISTRY_URL}
                    """
                }
            }
        }
    }

    post {
        failure {
            echo "Build failed"
        }
        success {
            echo "Image pushed: ${REGISTRY}/${IMAGE_NAME}:${TAG}"
        }
    }
}
