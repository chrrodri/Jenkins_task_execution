pipeline {
    agent any

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

        stage('Test SSH') {
            steps {
                sshagent(credentials: ['chrrodri-ssh-key']) {
                    sh '''
                        echo "SSH_AUTH_SOCK=$SSH_AUTH_SOCK"
                        ssh-add -l
                    '''
                }
            }
        }
    }
}