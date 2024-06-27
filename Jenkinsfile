pipeline {
    agent any

    tools {
        sonarQube 'SonarQube Scanner'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/glowcloudy/test.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    sonar-scanner \
                      -Dsonar.projectKey=your_project_key \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://localhost:9000 \
                      -Dsonar.login=sqp_e24527d6cac7ffc29a79f05458bfdf65a5b5b878
                    '''
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/*.jar', allowEmptyArchive: true
        }
    }
}
