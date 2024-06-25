pipeline {
    agent any

    stages {
        stage('Zip the File') {
            steps {
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
        }
    }
}

