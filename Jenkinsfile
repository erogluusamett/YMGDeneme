pipeline {
    agent any

    environment {
        BACKEND_DIR = 'backend'
        FRONTEND_DIR = 'frontend'
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Repo Jenkins tarafından otomatik klonlanacak.'
            }
        }

        stage('Build Backend Image') {
            steps {
                dir("${BACKEND_DIR}") {
                    script {
                        docker.build('yimg-backend', '.')
                    }
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir("${FRONTEND_DIR}") {
                    script {
                        docker.build('yimg-frontend', '.')
                    }
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                dir('YMGApp') {
                    bat 'docker-compose down --volumes || exit 0'
                    bat 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Uygulama başarıyla deploy edildi!'
        }
        failure {
            echo '❌ Bir hata oluştu. Kontrol edin.'
        }
    }
}
