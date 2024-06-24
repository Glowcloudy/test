pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'building the application...'
            }
        }
        stage('test') {
            steps {
                echo 'testing the application...'
            }
        }
        stage('deploy') {
            steps {
                echo 'deploying the application...'
            }
        }
          stage('SCM') {
              steps{
            checkout scm
              }
        }
        stage('SonarQube Analysis') {
            steps{
            def scannerHome = tool 'SonarQube';
            withSonarQubeEnv() {
              sh "${scannerHome}/bin/sonar-scanner"
            }
        }
        }
    }
}
