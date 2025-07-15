pipeline {
    agent any

    // triggers {
    //     pollSCM('H/2 * * * *') // Optional fallback; webhook preferred for real-time push detection
    // }

    environment {
        REGISTRY = "joerozen/my-docker-app-jenkins-1"
        IMAGE_NAME = "simple-py-app"
        TAG = "latest"
        CREDENTIALS_ID = "dockerhub-creds"
    }

    stages {
        stage('Checkout') {
            // when {
            //     branch 'main'
            // }
            steps {
                checkout scm
            }
        }

        stage('Debug Branch') {
            steps {
                script {
                    echo "Branch: ${env.BRANCH_NAME}"
                }
            }
        }   

        stage('Build Docker Image') {
            // when {
            //     branch 'main'
            // }
            steps {
                script {
                    sh "docker build -t ${REGISTRY}/${IMAGE_NAME}:${TAG} ."
                }
            }
        }

//         stage('Push Docker Image') {
//             // when {
//             //     branch 'main'
//             // }
//             steps {
//                 withCredentials([usernamePassword(credentialsId: env.CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
//                     sh """
//                         echo "$DOCKER_PASS" | docker login ${REGISTRY} -u "$DOCKER_USER" --password-stdin
//                         docker push ${REGISTRY}/${IMAGE_NAME}:${TAG}
//                         docker logout ${REGISTRY}
//                     """
//                 }
//             }
//         }
//     }

//     post {
//         failure {
//             echo "Build failed"
//         }
//         success {
//             echo "Image pushed: ${REGISTRY}/${IMAGE_NAME}:${TAG}"
//         }
//     }
// }
