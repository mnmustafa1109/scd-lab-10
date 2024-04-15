pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dckr_pat_1MQWXNoSSB2-4wNWku03zXo51Yo')
        DOCKER_IMAGE_NAME = 'mnmustafa1109/scd-lab-11'
    }


    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build("your-image-name:latest", "-f Dockerfile .")
                }
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        // Push Docker image to Docker Hub
                        docker.image("${DOCKER_IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy using Docker Compose
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            // Cleanup
            script {
                // Stop and remove containers after use
                sh 'docker-compose down'
            }
        }
    }
}
