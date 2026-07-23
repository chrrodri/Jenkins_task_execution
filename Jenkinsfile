pipeline {

    agent any

    options {
        timestamps()
        //ansiColor('xterm')
        skipStagesAfterUnstable()
        //timeout(time: 60, unit: 'MINUTES')
    }

    environment {
        CHRRODRI_TOKEN           = credentials('chrrodri-token')
    }

    stages {

        stage('BUILD') {
            steps {
                script {
                    echo "Building the project..."
                    // Add your build commands here
                }
            }
        }

    post { 
        always { 
            cleanWs()
        } 
    }    
}