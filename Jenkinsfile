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
                        echo "Key file: $SSH_KEY"
                        head -n 1 "$SSH_KEY"
                        tail -n 1 "$SSH_KEY"
                        wc -l "$SSH_KEY"
                        ssh-keygen -y -f "$SSH_KEY" > /tmp/jenkins_key.pub
                    '''
                }
            }
        }
    }
}