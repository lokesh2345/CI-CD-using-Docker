pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/lokesh2345/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp lokesh25434/samplewebapp:latest'
                //sh 'docker tag samplewebapp lokesh25434/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
		withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub',
        usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
      sh 'docker login -u "$USERNAME" -p "$PASSWORD"'
      cont.push()
    }
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 lokesh25434/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@192.168.216.142 run -d -p 8003:8080 lokesh25434/samplewebapp"
 
            }
        }
    }
	}
    
