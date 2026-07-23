pipeline {
    agent any

    options {
        timestamps()
        skipStagesAfterUnstable()
    }

    stages {
        stage('Prepare SSH') {
            steps {
                sh '''
                    mkdir -p ~/.ssh
                    ssh-keyscan -H 192.168.1.108 >> ~/.ssh/known_hosts
                    chmod 700 ~/.ssh
                    chmod 600 ~/.ssh/known_hosts
                '''
            }
        }

        stage('Connect to Server') {
            steps {
                sshagent(credentials: ['chrrodri-token']) {
                    sh '''
                        ssh chrrodri@192.168.1.108 "hostname && whoami"
                    '''
                }
            }
        }

        stage('Server Updates') {
            steps {
                sshagent(credentials: ['chrrodri-token']) {
                    sh '''
                        ssh chrrodri@192.168.1.108 "echo 'Updating server...' && sudo apt update && sudo apt upgrade -y"
                    '''
                }
            }
        }
    }
}