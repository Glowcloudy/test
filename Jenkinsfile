pipeline {
    agent any
    parameters {
        string(name: 'GIT_URL', defaultValue: 'http://github.com/glowcloudy/test.git', description: 'GIT_URL')
        booleanParam(name: 'VERBOSE', defaultValue: false, description: '')
    }
    
    environment {
        GIT_BUSINESS_CD = 'main'
        GITHUB_CREDENTIAL_ID = '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'
        VERBOSE_FLAG = '-q'
    }

    stages{
        stage('Preparation') { // for display purposes
            steps{
                script{
                    env.ymd = sh (returnStdout: true, script: ''' echo `date '+%Y%m%d-%H%M%S'` ''')
                }
                echo("params : ${env.ymd} " + params.tag)
            }
        }   

        stage('Checkout') {
            steps{
                git(branch: "${env.GIT_BUSINESS_CD}", 
                credentialsId: "${env.GITLAB_CREDENTIAL_ID}", url: params.GIT_URL, changelog: false, poll: false)
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


