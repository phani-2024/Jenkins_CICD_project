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
    }
}
