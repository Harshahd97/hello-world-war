pipeline {
    agent none
    stages {
        stage('Checkout') {
            steps {
                sh 'git clone https://github.com/Harshahd97/hello-world-war.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn --version'
                sh 'mvn clean install'
            }
        }
}
}
