pipeline {
    
    agent any

    environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-hub')
	}

    stages {

             stage('Login') {
			    steps {
				    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			    }
		    } 

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
                    sh 'docker logout'
                }
            }
        }
    }