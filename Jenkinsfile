pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh '''
                docker build -t abode-webapp .
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                docker rm -f test-container || true

                docker run -d \
                --name test-container \
                -p 8082:80 \
                abode-webapp
                '''
            }
        }

        stage('Production') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@65.1.147.87 "

                rm -rf website || true

                git clone https://github.com/RS-cloud-intellipaat/website.git

                cd website

                docker build -t abode-webapp .

                docker rm -f prod-container || true

                docker run -d \
                --name prod-container \
                -p 80:80 \
                abode-webapp

                "
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }

        failure {
            echo 'Pipeline execution failed'
        }
    }
}
