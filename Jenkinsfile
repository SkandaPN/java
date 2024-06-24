#!groovy
pipeline {
    environment {     
           registryCredentials = credentials('DBuild')
    }
    agent { label 'docker-node' }
    stages{
        stage('git-checkout') {
            steps {
                git branch: 'main', url:'https://github.com/SkandaPN/java.git'
            }
        }
        stage('Build docker image'){
            steps {
		        sh 'docker build -t ${registryCredentials_USR}/buildfreestyle:${BUILD_ID} .'
            }
        }
        stage('Push image to Hub'){
            steps {
                sh 'docker login -u ${registryCredentials_USR} -p ${registryCredentials_PSW}'
		        sh 'docker push ${registryCredentials_USR}/buildfreestyle:${BUILD_ID}'
            }
        }
        stage('Deploy ') {
            steps {
                sh 'docker run -itd --name cont-${BUILD_ID} -p 9000:8080 ${registryCredentials_USR}/buildfreestyle:${BUILD_ID}'
            }
            
        }
        
   }
}
