pipeline {
    agent { label 'slave' }
    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/Harshahd97/hello-world-war.git'
            }
        }
        stage('Build') {
            steps {
                dir("hello-world-war")
                sh 'docker run -t maven-build .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'rm -rf maven-build'
                sh 'docker run -d -p 8085:8080 --name tomcat-container maven-build'
            }
        }
    } 
  }   
