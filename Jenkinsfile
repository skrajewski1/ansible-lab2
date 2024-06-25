pipeline {
    agent any

    stages {
        stage('Zip the File') {
            steps {
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
            }
        }
        stage('Upload Artifacts to JFrog') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'jfrog-credentials', usernameVariable: 'JFROG_USER', passwordVariable: 'JFROG_PASS')]) {
                    sh '''curl -u$JFROG_USER:$JFROG_PASS -T \
                    ansible-${BUILD_ID}.zip \
                    "http://34.239.249.252:8081/artifactory/ansible/ansible-${BUILD_ID}.zip"'''
                }
            }
        }
    }
}