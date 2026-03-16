pipeline {
    environment {
    DOCKER_IMAGE = 'harishkumar09/fastapi-app:2.0.0'
    APP_NAME = 'harishkumar09/fastapi-app'
    TAG_VERSION = '3.0.0'
}
    agent any
    stages {
        stage('Docker Cred') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                   echo "${USER}"
               }
            }
        }
          stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                   echo "Logging into Docker"
                   sh 'docker login -u ${USER} -p ${PASS}'
                   echo "======================================="
                   echo "Docker login completed successfully"
                   echo "======================================="
               }
            }
        }
        stage('Docker Pull') {
            steps {
                    echo "Pulling Docker image"
                    sh "docker pull ${DOCKER_IMAGE}"
                    echo "======================================="
                    echo "Docker Pull completed successfully"
                    echo "======================================="
                }
            }
        stage('Docker Tag') {
            steps {
                    echo "Docker image tagging in progress"
                    sh   "docker tag ${DOCKER_IMAGE} ${APP_NAME}:${TAG_VERSION}"
                    echo "======================================="
                    echo "Docker tag completed successfully"
                    echo "======================================="
                }
        }
        stage('Docker Push') {
            steps {
                    echo "Docker image Push in progress"
                    sh   "docker push ${APP_NAME}:${TAG_VERSION}"
                    echo "======================================="
                    echo "Docker Push successfully"
                    echo "======================================="
                }
                }       
    }
}
