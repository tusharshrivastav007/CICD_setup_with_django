pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_PATH = '/path/to/your/docker-compose.yml'
        PROJECT_DIR = '/path/to/your/project'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling latest code...'
                git branch: 'main', url: 'https://gitlab.com/<your_repo>.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh 'docker-compose build'
                }
            }
        }

        stage('Stop Existing Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh 'docker-compose down'
                }
            }
        }

        stage('Deploy New Containers') {
            steps {
                dir("${PROJECT_DIR}") {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
