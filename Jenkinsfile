pipeline {
    
    agent any

    environment {
        DOCKER_HUB_CREDS = credentials ('docker-hub')
    }

    stages {
            stage('Building Docker Image') {
                steps {
                    dir('/var/lib/jenkins/workspace/ui-pipeline/node/') {
                        sh "docker build -t andresvelez11/movie-analyst-ui ."
                    }

                    dir('/var/lib/jenkins/workspace/ui-pipeline/nginx/') {
                        sh "docker build -t andresvelez11/movie-analyst-nginx ."
                    }
                }
            }

            stage('Deploying Docker Image to Dockerhub') {
                steps {
                    sh 'docker push andresvelez11/movie-analyst-ui:latest'

                    sh 'docker push andresvelez11/movie-analyst-nginx:latest'
                }
            }
        }
    }
}