pipeline {
    agent { label 'docker' }
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
                sh 'sudo docker build -t tomcat-file:1.0 .'
            }
        }
    }
        stage('Deploy') {
            steps {
                sh 'sudo docker rm -f tomcat-file'
                sh 'sudo docker run -d -p 8085:8080 --name tomcat-container tomcat-file:1.0'
            }
        }
    } 
  }   
