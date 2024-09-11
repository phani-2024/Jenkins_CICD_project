#!groovy
pipeline {
    agent { label 'ubuntu' }
    tools {
          maven 'maven'
}
    stages {
        stage('validate') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('upload_to_nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'webapp_project', classifier: '', file: './target/*.war', type: 'war']],
                credentialsId: 'Nexus-creditials',
                groupId: 'com.phani.cloud',
                nexusUrl: '18.212.247.249:8081/',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'snapshotRepo',
                version: '1.3-SNAPSHOT'
        }
    }
        stage('deploy_into_tomcat7') {
            steps {
               deploy adapters: [tomcat7(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.196.183.85:8081/')],
               contextPath: 'Project-webapp',
               war: '**/target/*.war'
            }
        }
        stage('post-build') {
            steps {
               emailext body: '''The automated test report for ${JOB_NAME} executed via Jenkins has finished its latest run.
               - Job Name: ${JOB_NAME}
               - Job Status: ${BUILD_STATUS}
               - Job Number: ${BUILD_NUMBER}
               - Job URL: ${BUILD_URL}
               Please refer to the build information above for additional details.
               This email is generated automatically by the system.
               Thanks''',
               attachLog : true
               subject: 'API Test Report as of ${BUILD_NUMBER} - ${JOB_NAME}',
               to: 'phanikanaparthi@gmail.com'
            
            }



}
}
