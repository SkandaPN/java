#!groovy
pipeline {
    environment {     
           registryCredentials = credentials('Docker_credential')
    }
    agent { label 'docker' }
    stages{
        stage('git-checkout') {
            steps {
                git branch: 'master', url:'https://github.com/Nithishkumar0064/new-javafile.git'
            }
        }
        stage('Build docker image'){
            steps {
		        sh 'docker build -t ${registryCredentials_USR}/tomcat4:${BUILD_ID} .'
            }
        }
        stage('Push image to Hub'){
            steps {
                sh 'docker login -u ${registryCredentials_USR} -p ${registryCredentials_PSW}'
		        sh 'docker push ${registryCredentials_USR}/tomcat4:${BUILD_ID}'
            }
        }
        stage('Deploy ') {
            steps {
                sh 'docker run -itd --name cont-${BUILD_ID} -p 8000:8080 ${registryCredentials_USR}/tomcat4:${BUILD_ID}'
            }
            
        }
        
   }
}
