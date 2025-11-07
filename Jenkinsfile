pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_PATH = '/home/asus/Projects/CICD/django-docker-compose/docker-compose.yml'
        PROJECT_DIR = '/home/asus/Projects/CICD/django-docker-compose'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling latest code...'
                git branch: 'main', url: 'https://github.com/tusharshrivastav007/CICD_setup_with_django.git'
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
            echo '✅ Deployment successful! Yes Tushar you did it ....'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
