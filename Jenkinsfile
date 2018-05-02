pipeline {
    agent any
    environment {
        // Slack variables
        SLACK_BASEURL = 'https://testingjenkinsgroup.slack.com/services/hooks/jenkins-ci/'
        SLACK_TOKEN = "5lyVojwh3kSmvacBPNFz6wl2"
    }    
    stages {
        stage('Build') {
                steps {
                    git url: 'https://github.com/mm54760/TOH.git'
                    sh '''
                    npm config ls
                    node -v
                    npm config set registry https://nexushdq.aa.com/repository/registry.npmjs-proxy/
                    npm install 
                    sh 'env'
                    '''
                }
                post {
                    success {
                        slackSend channel: "#general", message: "Successful build ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
                    }
                    failure{
                        slackSend channel: "#general", message: "The pipeline ${currentBuild.fullDisplayName} completed successfully.", color: '#00FF00', token: "5lyVojwh3kSmvacBPNFz6wl2", baseUrl: "https://testingjenkinsgroup.slack.com/services/hooks/jenkins-ci/"
                    }
                }     
        }
    }
}