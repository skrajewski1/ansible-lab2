pipeline {
    agent any

    stages {
        stage('Zip the File') {
            steps {
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
            }
        }
        stage('upload artifacts to jfrog')
            steps{
                sh 'curl -uadmin:AP8gcgmmset5jeYChTJYDN6XmDd -T \
                ansible-${BUILD_ID}.zip \
                "http://34.239.249.252:8081/artifactory/ansible/ansible-${BUILD_ID}.zip"'
            }
    }
}

