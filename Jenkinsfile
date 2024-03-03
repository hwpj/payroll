pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dkhw'
        DOCKER_REGISTRY = 'images'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checks out the source code from GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean and install
                script {
                    sh './mvnw clean install'
                }
            }
        }

        stage('Docker Build') {
            steps {
                // Build the Docker image
                script {
                    sh "docker build -t ${DOCKER_REGISTRY}/${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Docker Push') {
            steps {
                // Push the Docker image to the registry
                script {
                    sh "docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        always {
            echo 'post pipeline:'
        }
        success {
            echo 'successful'
        }
        failure {
            echo 'fail'
        }
    }
}
