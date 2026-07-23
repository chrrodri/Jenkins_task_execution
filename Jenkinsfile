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
                    sh 'sudo apt-get update -y'
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