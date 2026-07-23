pipeline {
    agent any

    options {
        timestamps()
    }

    stages {
        stage('Test SSH') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: 'chrrodri-ssh-key',
                        keyFileVariable: 'SSH_KEY',
                        usernameVariable: 'SSH_USER'
                    )
                ]) {
                    sh '''
                        mkdir -p ~/.ssh
                        ssh-keyscan -H 192.168.1.108 >> ~/.ssh/known_hosts
                        chmod 700 ~/.ssh
                        chmod 600 ~/.ssh/known_hosts

                        ssh -i "$SSH_KEY" -o IdentitiesOnly=yes -o BatchMode=yes "$SSH_USER@192.168.1.108" "hostname && whoami"
                    '''
                }
            }
        }
    }
}