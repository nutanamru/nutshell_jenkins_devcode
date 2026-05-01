pipeline {
	agent any
	
	environment {
		DOCKER_IMAGE = 'hello-world-java'
		IMAGE_TAG = '1.0'
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
					sh "docker push ${DOCKER_IMAGE}:${IMAGE_TAG}"
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

