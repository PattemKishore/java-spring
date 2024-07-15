pipeline {
    agent any
    stages {
       stage('maven build ') {
           steps {
                sh 'mvn clean package'
           }
        }
 
        stage('docker image build ') {
           steps {
                sh 'docker build -t java-spring-19:v{BUILD_NUMBER} .'
            }
        }
        stage('docker login ') {
           steps {
                sh 'docker login '
           }
        }
        stage('docker tagging ') {
           steps {
                sh 'docker tag java-spring-19:v{BUILD_NUMBER} kishorepattem/devops19:spring-19.{BUILD_NUMBER}'
 
           }
        }
        stage('image push dockerhub') {
           steps{
                sh 'docker push kishorepattem/devops19:spring-19.{BUILD_NUMBER}'
           }
         }
        stage('push ECR'){
            steps {
                sh '''aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 299250580675.dkr.ecr.us-west-2.amazonaws.com
           		    
			                 docker tag devops19:v${BUILD_NUMBER} 299250580675.dkr.ecr.us-west-2.amazonaws.com/devops19-java:v${BUILD_NUMBER}
                    	 docker push 299250580675.dkr.ecr.us-west-2.amazonaws.com/devops19-java:v${BUILD_NUMBER}
		   
       '''
        
        }
}
    }
}
