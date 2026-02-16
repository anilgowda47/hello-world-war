pipeline {
    agent any

    environment {
        IMAGE_NAME = "anil/hello-world-war"
        IMAGE_TAG  = "${BUILD_NUMBER}"
        CONTAINER_NAME = "hello-world-war-doc-cntr"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master',
                url: 'https://github.com/anilgowda47/hello-world-war.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true

                docker run -d \
                --name ${CONTAINER_NAME} \
                -p 8088:8080 \
                ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }
}
