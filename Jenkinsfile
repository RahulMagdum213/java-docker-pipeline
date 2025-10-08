https://github.com/RahulMagdum213/java-docker-pipeline.git
pipeline {
    agent any

    environment {
        // Use your Jenkins Credentials ID
        DOCKERHUB_CREDENTIALS = 'dockerhub-login'
        DOCKER_IMAGE = "rahul1584/ise3"
    }

    stages {
        stage('Checkout') {
            steps {
                bat 'git checkout main && git pulls https://github.com/RahulMagdum213/java-docker-pipeline.git'
            }
        }

        stage('Build Java App') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE%:latest ."
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CREDENTIALS}", 
                                                      usernameVariable: 'rahul1584', 
                                                      passwordVariable: '@Docker123')]) {
                        bat """
                        echo %PASSWORD% | docker login -u %USERNAME% --password-stdin
                        docker push %DOCKER_IMAGE%:latest
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Docker Image built and pushed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs."
        }
    }
}
