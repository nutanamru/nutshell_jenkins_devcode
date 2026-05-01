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
				sh 'javac hello.java'
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

