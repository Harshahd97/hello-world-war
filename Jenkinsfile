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
                sh 'docker build -t tomcat-file:$BUILD_NUMBER .'
				}
			}
		}
		
        stage('Login to Docker Hub') {         
			steps{                            
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
				echo 'Login Completed'                
			}           
		}               
		stage('Push Image to Docker Hub') {         
			steps{                            
				sh 'sudo docker push harshahd18/newrepo_20_03:$BUILD_NUMBER'  
				echo 'Push Image Completed'       
			}           
		}
		stage('Pull Image and Deploy') {
            agent any
            steps {
                sh "docker pull harshahd18/newrepo_20_03:${BUILD_NUMBER}"
                sh "docker run -d --name my_container -p 8085:8080 harshahd18/newrepo_20_03:${BUILD_NUMBER}"
			}
		}
	}
}
