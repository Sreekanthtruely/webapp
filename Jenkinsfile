pipeline {
    agent {
    docker {
      image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
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
                // sh 'docker tag samplewebapp sragro/samplewebapp:latest'
                sh 'docker tag samplewebapp sragro/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
         steps {
          withDockerRegistry([ credentialsId: "DockerHub", url: "" ]) {
          // sh  'docker push sragro/samplewebapp:latest'
          sh  'docker push sragro/samplewebapp:$BUILD_NUMBER' 
	}
	    }
  }
 }
}
        
     
    
