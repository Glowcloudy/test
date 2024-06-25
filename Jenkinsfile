pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/glowcloudy/test.git'
            }
        }
        
        stage('Change application.yml') {
            steps {
                sh 'rm ./src/main/resources/application.properties'
                sh 'cp /home/env/application.properties /var/lib/jenkins/workspace/pipeline/src/main/resources'
            }
        }
        
        stage('Gradle Build') {
            steps {
                sh './gradlew clean bootJar'
            }
        }
    }
}
