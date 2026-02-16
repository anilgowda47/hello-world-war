stages {

    stage('Checkout Code') {
        steps {
            git branch: 'master',
            url: 'https://github.com/anilgowda47/hello-world-war.git'
        }
    }

    stage('Build WAR') {
        steps {
            sh 'mvn clean package'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
        }
    }

    stage('Login to Docker Hub') {
        steps {
            withCredentials([usernamePassword(
                credentialsId: DOCKER_CREDS,
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'
            )]) {
                sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
            }
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
