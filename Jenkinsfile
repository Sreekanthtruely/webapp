pipeline {
    agent any
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Sreekanthtruely/webapp.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp sragro/samplewebapp:latest'
                //sh 'docker tag samplewebapp sragro/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "DockerHub", url: "" ]) {
          sh  'docker push sragro/samplewebapp:latest'
        //  sh  'docker push sragro/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 sragro/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@13.233.32.108 run -d -p 8003:8080 sragro/samplewebapp"
 
            }
        }
    }
	}
    
