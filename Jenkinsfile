pipeline {
    
    agent {
        label "pipeline"
    }
    
    
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/wssrronak/java-docker-app.git'
                
            }
            
        }
        
        stage('Build by Maven Package') {
            steps {
                sh 'sudo mvn dependency:purge-local-repository'
                sh 'sudo mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                   sh 'sudo docker build -t srronak_java:$BUILD_TAG .'
                }
        }
	stage("Pushing Image to docker HUB") {
		steps {
			withCredentials([string(credentialsId: 'docker-hub-passwd', variable: 'docker_hub_var')]) {
 				sh 'sudo docker login -u srronak -p ${docker_hub_var}'
				sh 'sudo docker tag srronak_java:$BUILD_TAG srronak/java:$BUILD_TAG'
				sh 'sudo docker push srronak/java:$BUILD_TAG'
			}
		}
	}
	stage("Deploy webapp in QAT Env") {
		steps {
			sshagent(['QA_ENV_SSH_CRED']) {
				sh 'ssh -o StrictHostKeyChecking=false ubuntu@13.233.125.120  sudo docker run -dit -p 8080:8080 --name javaapp srronak/java:$BUILD_TAG'
				}
		}
	}
    }
}
