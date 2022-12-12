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
                   sh 'docker build -t srronak_java:$BUILD_TAG .'
                }
        }
    }
}
