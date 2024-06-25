pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps{
                checkout({$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/glowcloudy/test.git']]])
            }
        }
        stage('SonarQube analysis') {
            steps{
                withSonarQubeEnv('SonarQube'){
                    sh "mvn sonar:sonar -Dsonar.projectKey=test -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_82c669f2d0c99eb5984983bbec54210f7fc71b2f"
                }
            }
        }
}
}

