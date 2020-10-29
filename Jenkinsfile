pipeline {
    agent any
	

 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/cpbarik1/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp cpbarik1/samplewebapp:latest'
                //sh 'docker tag samplewebapp cpbarik1/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub1", url: "" ]) {
          sh  'docker push cpbarik1/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 cpbarik1/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.105.60.5 run -d -p 8003:8080 cpbarik1/samplewebapp"
 
            }
        }
    }
	}
    
