pipeline {
	agent {	
		label 'pipeline-1'
		}
	stages {
		stage("SCM") {
			steps {
				sh 'git https://github.com/wssrronak/java-docker-app.git'
				}
			}
		stage("build") {
			steps {
				sh 'sudo mvn clean package'
				}
			}
		}
	}
