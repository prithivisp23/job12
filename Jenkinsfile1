@Library('jenkins-shared-library') _

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    mySharedLibrary.buildJavaApp()
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    mySharedLibrary.testJavaApp()
                }
            }
        }
    }
}
