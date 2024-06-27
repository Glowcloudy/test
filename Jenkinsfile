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

        stage('Build') {
            steps {
                sh './gradlew build' // Gradle 사용 시
                // 또는 sh 'mvn clean install' // Maven 사용 시
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh './gradlew sonarqube' // Gradle 사용 시
                    // 또는 sh 'mvn sonar:sonar' // Maven 사용 시
                }
            }
        }
    }

    post {
        always {
            junit '**/build/test-results/test/*.xml' // 테스트 결과 보고서
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true
        }
    }
}
