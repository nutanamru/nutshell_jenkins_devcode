pipeline {
	agent any
	
	environment {
		DOCKER_IMAGE = 'hello-world-java'
		IMAGE_TAG = 'latest'
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
						sh "docker build -t  nutanamru52/${DOCKER_IMAGE}:${IMAGE_TAG} ."
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
									usernameVariable: 'DOCKER_USERNAME',
									passwordVariable: 'DOCKER_PASSWORD')]) {
						sh """
						echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
						echo "Login Sucessfull on Docker Hub"
						docker push "nutanamru52/${DOCKER_IMAGE}:${IMAGE_TAG}"
						"""
					}
				}
			}
		}

		stage('kubernetes deployment') {
			steps {
				script {
					sh "kubectl apply -f deployment.yml"
					sh "kubectl apply -f service.yml"
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

