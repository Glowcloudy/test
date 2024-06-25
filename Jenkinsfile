pipeline {
    agent any
    parameters {
        string(name: 'GIT_URL', defaultValue: 'http://github.com/glowcloudy/test.git', description: 'GIT_URL')
        booleanParam(name: 'VERBOSE', defaultValue: false, description: '')
    }
    
    environment {
        GIT_BUSINESS_CD = 'main'
        GITHUB_CREDENTIAL_ID = 'glowcloudy'
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
