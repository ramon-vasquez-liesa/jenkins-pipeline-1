pipeline {
    agent any

    environment {
        IMAGE_NAME       = 'test-img'
        DOCKERHUB_USER   = 'ramonvasquezliesa'
        DOCKERHUB_REPO   = "${DOCKERHUB_USER}/${IMAGE_NAME}"
        TAG              = 'latest'
    }

    stages {
        stage('Build Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}", '-f Dockerfile .')
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${DOCKERHUB_USER}/${IMAGE_NAME}").push("${TAG}")
                    }
                }
            }
        }
    }
}
