node {
    stage('Clone') {
        git branch: 'main', credentialsId: 'your-credentials-id', url: 'https://github.com/your-org/your-repo.git'
    }
    
    stage('Change application.yml') {
        // Verify the existence of the source file
        sh 'ls -l /home/env/application.properties'
        
        // Copy the file (if it exists) to the correct destination
        sh 'cp /home/env/application.properties ./src/main/resources/application.properties'
    }
    
    stage('Run SonarQube Analysis') {
        def scannerHome = tool 'SonarQube'
        withSonarQubeEnv(credentialsId: 'sqp_82c669f2d0c99eb5984983bbec54210f7fc71b2f', installationName: 'SonarQube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
}
