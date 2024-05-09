pipeline {
	agent {
		node {
			label 'master'
		}
	}

	tools {
		maven 'maven3'
	}

	options {
		buildDiscarder logRotator(
					daysToKeepStr: '15',
					numToKeepStr: '10'
			)
	}

	environment {
		APP_NAME = "STUDENT_APP"
		APP_ENV  = "DEV"
	}

	stages {

		stage('Cleanup Workspace') {
			steps {
				cleanWs()
				sh """
				echo "Cleaned Up Workspace for ${APP_NAME}"
				"""
			}
		}

		stage('Code Checkout') {
			steps {
				checkout([
					$class: 'GitSCM',
					branches: [[name: '*/main']],
					userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
				])
			}
		}

		stage('Code Build') {
			steps {
				 sh 'mvn install -Dmaven.test.skip=false'
			}
		}

		stage('Printing All Global Variables') {
			steps {
				sh """
				env
				"""
			}
		}

	}
}
