pipeline {
    agent any

    stages {
        stage('Test SSH') {
            steps {
                sh '''
                    mkdir -p ~/.ssh
                    ssh-keyscan -H 192.168.1.108 >> ~/.ssh/known_hosts
                '''

                sshagent(credentials: ['chrrodri-token']) {
                    sh '''
                        ssh chrrodri@192.168.1.108 "hostname && whoami"
                    '''
                }
            }
        }
    }
}