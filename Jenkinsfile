pipeline {
	agent any
	
	environment {
		DOCKER_IMAGE = 'hello-world-java-1'
		DOCKER_TAG = '1.0'
	}
	
	stages {
		stage('Checkout') {
			steps {
				git branch: 'main', url:'https://github.com/nutanamru/nutshell_jenkins_devcode.git'
			}
		}

		stage('Docker Build') {
			steps {
				script {
					if (fileExists('Dockerfile')) {
						sh "docker build -t ${env.DOCKER_IMAGE} ."
					} else {
						error "Docker file not found"
					}
				}
			}
		}

		stage('push to deockerhub') {
			steps {
				script {
					withCredentials([usernamePassword(credentialsId: 'my-docker-hub-credentials-id',
									usernameVariable: 'nutanamru52',
									passwordVariable: 'Tosti@052')]) {
						sh """
						echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
						echo "Login Sucessfull on Docker Hub"
						docker push ${env.DOCKER_IMAGE}:${env.IMAGE_TAG}"
						"""
					}
				}
			}
		}
 
	}


	post {
		success {
			echo 'Docker image build successfully.'
		}
		failure {
			echo 'Docker image build failed.'
		}
	}
}

