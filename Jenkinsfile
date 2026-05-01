pipeline {
	agent any
	
	stages {
		stage('Checkout') {
			steps {
				git branch: 'main', url:'https://github.com/nutanamru/nutshell_jenkins_devcode.git'
			}
		}

		stage('run java code') {
			steps {
				sh 'javac HelloWorld.java'
				sh 'java HelloWorld'
			}
		}
	}

	post {
		success {
			echo 'Java code build successfully.'
		}
		failure {
			echo 'Java code build failed.'
		}
	}
}

