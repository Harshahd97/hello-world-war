pipeline {
    agent { label 'slave2' }
    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/Harshahd97/hello-world-war.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn --version'
                sh 'mvn clean install'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ssh root@172.31.21.167'
                sh 'scp /home/slave2/workspace/pipeline_job_1/target/hello-world-war-1.0.0.war root@172.31.21.167:/home/ubuntu/apache-tomcat-8.5.98/webapps/'
            }
        }
    } 
  }   
