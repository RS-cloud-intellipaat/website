pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Website...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Website...'
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                sshagent(['production-ssh']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@13.206.107.104 "
                    sudo cp -r * /var/www/html/
                    "
                    '''
                }
            }
        }
    }
}
