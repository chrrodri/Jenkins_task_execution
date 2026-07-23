pipeline {

    agent any

    options {
        timestamps()
        //ansiColor('xterm')
        skipStagesAfterUnstable()
        //timeout(time: 60, unit: 'MINUTES')
    }

/*     environment {
        CHRRODRI_TOKEN           = credentials('chrrodri-token')
    } */

    stages {

        stage('Server Updates') {
            steps {
                script {
                    echo "Updating server..."
                    sh '''
                        ssh chrrodri@192.168.1.108 "echo 'Updating server...'; sudo apt update && sudo apt upgrade -y"
                    '''
                    // Add your build commands here
                }
            }
        }

/*         post { 
            always { 
                cleanWs()
            } 
        }  */
    }   
}