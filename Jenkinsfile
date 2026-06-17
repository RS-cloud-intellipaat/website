pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t abode-webapp .'
            }
        }

        stage('Test') {
            steps {
                sh '''
                docker rm -f test-container || true
                docker run -d --name test-container -p 8082:80 abode-webapp
                '''
            }
        }

        stage('Production') {
       
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@65.1.147.87 "
                docker rm -f prod-container || true
                docker run -d --name prod-container -p 80:80 abode-webapp
                "
                '''
            }
        }
    }
}
