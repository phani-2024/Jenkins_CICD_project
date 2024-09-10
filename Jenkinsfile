#!groovy
pipeline {
    agent any
    tools {
          maven 'maven'
}
    stages {
        stage('01-validate') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('02-compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('03-test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('04-package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('05-upload') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'webapp_project', classifier: '', file: '/var/lib/jenkins/workspace/testingJob/target/webapp_project.war', type: 'war']], 
                credentialsId: 'Nexus-creditials', 
                groupId: 'com.phani.cloud', 
                nexusUrl: '107.22.139.151:8081/', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'snapshotRepo', 
                version: '1.2-SNAPSHOT'
        }
    }
        stage('06-deploy_into_tomcat7') {
            steps {
               deploy adapters: [tomcat7(credentialsId: 'tomcat-credentials', path: '', url: 'http://107.21.53.147:8081/')], 
               contextPath: 'sample-webapp', 
               war: '**/target/*.war'
            }
            }



}
}
