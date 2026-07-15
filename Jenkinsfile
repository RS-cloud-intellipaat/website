pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Application...'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'master'
            }
            steps {
                sshagent(credentials: ['production-ssh']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@13.206.107.104 << EOF
                    sudo cp -r * /var/www/html/
                    EOF
                    '''
                }
            }
        }
    }
}
