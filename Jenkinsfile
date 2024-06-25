node {
    stage('Clone') {
        git branch: 'main', credentialsId: 'your-credentials-id', url: 'https://github.com/your-org/your-repo.git'
    }
       
    stage('Run SonarQube Analysis') {
        def scannerHome = tool 'SonarQube'
        withSonarQubeEnv(credentialsId: 'sqp_82c669f2d0c99eb5984983bbec54210f7fc71b2f', installationName: 'SonarQube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
}

