pipeline {
    agent any

    parameters {
        string(name: 'SSH_HOST', defaultValue: '192.168.1.108')
        string(name: 'SSH_USER', defaultValue: 'chrrodri')
        credentials(name: 'SSH_CREDENTIALS', defaultValue: 'chrrodri-ssh-key')
    }

    stages {
        stage('Remote Test') {
            steps {
                script {
                    def remote = [
                        name: 'target-server',
                        host: params.SSH_HOST,
                        user: params.SSH_USER,
                        allowAnyHosts: true
                    ]

                    withCredentials([
                        sshUserPrivateKey(
                            credentialsId: params.SSH_CREDENTIALS,
                            keyFileVariable: 'SSH_KEY'
                        )
                    ]) {
                        remote.identityFile = SSH_KEY

                        sshCommand remote: remote, command: 'hostname && whoami'
                    }
                }
            }
        }
    }
}