pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'laravel-app-image'
        DOCKER_CONTAINER = 'laravel-app-container'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Laravel application code from version control (e.g., Git)
                // For example, if you're using Git:
                git 'https://github.com/your-username/laravel-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image for Laravel application
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run Laravel tests inside the Docker container
                    sh "docker run --rm ${DOCKER_IMAGE} php artisan test"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Stop and remove any previous containers with the same name
                    sh "docker stop ${DOCKER_CONTAINER} || true"
                    sh "docker rm ${DOCKER_CONTAINER} || true"

                    // Run the Laravel application in a Docker container
                    sh "docker run -d -p 80:80 --name ${DOCKER_CONTAINER} ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
