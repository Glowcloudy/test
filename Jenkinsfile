pipeline {
    agent any

    environment {
        // SonarQube 서버 설정 (SonarQube 서버 이름을 Jenkins 설정에서 등록한 이름으로 대체)
        SONARQUBE_SERVER = 'SonarQube'
        // SonarQube 프로젝트 키 설정 (SonarQube에서 프로젝트를 식별하기 위한 고유 키)
        SONARQUBE_PROJECT_KEY = 'sqp_82c669f2d0c99eb5984983bbec54210f7fc71b2f'
    }

    stages {
        stage('Checkout') {
            steps {
                // GitHub에서 프로젝트를 체크아웃
                git 'https://github.com/glowcloudy/test.git'
            }
        }

        stage('Build') {
            steps {
                // Maven을 사용하여 프로젝트 빌드
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Maven을 사용하여 SonarQube 분석 수행
                withSonarQubeEnv(SONARQUBE_SERVER) {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=${sqp_82c669f2d0c99eb5984983bbec54210f7fc71b2f}'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                // SonarQube의 Quality Gate 통과 여부를 확인 (실패 시 빌드 중지)
                script {
                    timeout(time: 1, unit: 'HOURS') {
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }
    }

    post {
        always {
            // 빌드 후 작업 (예: 로그 정리, 이메일 알림 등)
            echo 'Pipeline completed.'
        }
    }
}
