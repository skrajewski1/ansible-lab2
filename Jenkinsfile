pipeline {
    agent any

    stages {
        stage('Zip the File') {
            steps {
                sh 'rm -rf *.zip || echo ""'
                sh 'zip -r ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
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
        stage('publish to ansible server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible-server', \
                transfers: [sshTransfer(cleanRemote: false, excludes: '', \
                execCommand: 'unzip -o ansible-${BUILD_ID}.zip; rm -rf ansible-${BUILD_ID}.zip', \
                execTimeout: 120000000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, \
                patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, \
                removePrefix: '', sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false, \
                useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
