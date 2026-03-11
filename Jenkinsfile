pipeline{
    agent {
        label 'AGENT-1'
    }
    environment{
        appVersion = ''
        REGION = "us-east-1"
        ACC_ID = "430774481266"
        PROJECT= "roboshop"
        COMPONENT = "catalogue"
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    stages{
        stage('Deployment'){
            steps{
                script{
                     withAWS(credentials: 'aws-cred', region: 'us-east-1') {
                        sh """
                           aws eks update-kubeconfig --region ${REGION} --name ${PROJECT}
                        """
                    }
                }
            }
        }
        
    }
    post{
        always{
            deleteDir()
        }
    }
}