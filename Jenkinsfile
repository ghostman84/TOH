pipeline {
    agent any
    // environment {

    // }    
    stages {
        stage('Build') {
            steps {
                git url: 'https://github.com/mm54760/TOH.git'
                sh '''
                npm config ls
                node -v
                npm config set registry https://nexushdq.aa.com/repository/registry.npmjs-proxy/
                npm install 
                '''
            }
            post {
                success {
                    slackSend channel: "#general", message: "The pipeline ${currentBuild.fullDisplayName} completed successfully.", color: '#00FF00', token: "5lyVojwh3kSmvacBPNFz6wl2", baseUrl: "https://testingjenkinsgroup.slack.com/services/hooks/jenkins-ci/"
                }
            }                
        }
    }
}