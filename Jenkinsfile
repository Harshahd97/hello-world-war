pipeline {
    agent { label 'docker' }
    environment {     
    DOCKERHUB_CREDENTIALS= credentials('dockerhubcredentials')     
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/Harshahd97/hello-world-war.git'
            }
        }
		
        stage('Build') {
            steps {
                sh 'echo "inside build"'
                dir("hello-world-war") {
                sh 'echo "inside dir"'    
                sh 'docker build -t tomcat-file:${BUILD_NUMBER} .'
				}
			}
		}
		
        stage('Login to Docker Hub') {         
			steps{                            
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
				echo 'Login Completed'                
			}           
		}               
		stage('Push Image to Docker Hub') {         
			steps{  
				sh "docker tag tomcat-file:${BUILD_NUMBER} harshahd18/newrepo_20_03:${BUILD_NUMBER}"
				sh "docker push harshahd18/newrepo_20_03:${BUILD_NUMBER}"                 
				echo 'Image pushing completed..'       
			}           
		}
	}
}
