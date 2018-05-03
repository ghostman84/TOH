pipeline {
    agent any
    environment {
        JOB_NAME  = "Test TOH"

        // Slack variables
        SLACK_BASEURL = 'https://testingjenkinsgroup.slack.com/services/hooks/jenkins-ci/'
        SLACK_TOKEN = "5lyVojwh3kSmvacBPNFz6wl2"

        //GitHub 
        GIT_URL = "'https://github.com/mm54760/TOH.git'"
    }    
    stages {
        stage('Checkout') {
            steps {
                 deleteDir()
                 git url: ${env.GIT_URL}
            }            
            post {
                success {
                    notifySlack("Successful Checkout")
                    //slackSend channel: "#general", message: "Successful Checkout ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
                }
                failure{
                    notifySlack("Checkout failed")
                    //slackSend channel: "#general",  message: "Checkout failed  ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
                }
            }                 
        }
        stage('Build') {
            steps {
                sh '''
                npm config ls
                node -v
                npm config set registry https://nexushdq.aa.com/repository/registry.npmjs-proxy/
                npm install 
                ng build
                '''
            }
            post {
                success {
                    notifySlack("Successful Build")
                    // slackSend channel: "#general", message: "Successful Checkout ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
                }
                failure{
                    notifySlack("Failed Build")
                    // slackSend channel: "#general",  message: "Checkout failed  ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#FF0000', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
                }
            }                 
        }
        // stage('PushToCloud') {
        //     steps {
        //         sh '''
        //         cf push
        //         '''
        //     }
        //     post {
        //         success {
        //             slackSend channel: "#general", message: "Successful Checkout ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
        //         }
        //         failure{
        //             slackSend channel: "#general",  message: "Checkout failed  ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
        //         }
        //     }                 
        // }

    }
}


def notifySlack(String message){
    slackSend channel: "#general", message: "${message} ${env.JOB_NAME} ${env.BUILD_NUMBER}", color: '#00FF00', token: "${env.SLACK_TOKEN}", baseUrl: "${env.SLACK_BASEURL}"
}