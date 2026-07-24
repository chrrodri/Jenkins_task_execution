pipeline {
    agent any

    parameters {
        string(
            name: 'SSH_USER',
            defaultValue: 'chrrodri',
            description: 'Usuario SSH del servidor'
        )

        string(
            name: 'SSH_HOST',
            defaultValue: '192.168.1.108',
            description: 'IP o hostname del servidor'
        )

        credentials(
            name: 'SSH_CREDENTIALS',
            defaultValue: 'chrrodri-ssh-key',
            description: 'Credencial SSH de Jenkins',
            credentialType: 'com.cloudbees.jenkins.plugins.sshcredentials.impl.BasicSSHUserPrivateKey',
            required: true
        )

        choice(
            name: 'ACTION',
            choices: ['test', 'update', 'upgrade'],
            description: 'Accion a ejecutar'
        )
    }

    stages {
        stage('Prepare SSH') {
            steps {
                sh '''
                    mkdir -p ~/.ssh
                    ssh-keyscan -H "$SSH_HOST" >> ~/.ssh/known_hosts
                    chmod 700 ~/.ssh
                    chmod 600 ~/.ssh/known_hosts
                '''
            }
        }

        stage('Run Remote Command') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: "${params.SSH_CREDENTIALS}",
                        keyFileVariable: 'SSH_KEY',
                        usernameVariable: 'SSH_CRED_USER'
                    )
                ]) {
                    sh '''
                        if [ "$ACTION" = "test" ]; then
                            REMOTE_CMD="hostname && whoami"
                        elif [ "$ACTION" = "update" ]; then
                            REMOTE_CMD="sudo -n apt update"
                        elif [ "$ACTION" = "upgrade" ]; then
                            REMOTE_CMD="sudo -n apt update && sudo -n apt upgrade -y"
                        else
                            echo "Accion invalida: $ACTION"
                            exit 1
                        fi

                        ssh -i "$SSH_KEY" \
                            -o IdentitiesOnly=yes \
                            -o BatchMode=yes \
                            "$SSH_USER@$SSH_HOST" \
                            "$REMOTE_CMD"
                    '''
                }
            }
        }
    }
}