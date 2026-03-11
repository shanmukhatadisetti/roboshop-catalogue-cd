pipeline{
    agent {
        label 'AGENT-1'
    }
    environment{
    
        REGION = "us-east-1"
        ACC_ID = "430774481266"
        PROJECT= "roboshop"
        COMPONENT = "catalogue"
    }
    options{
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'appVersion', description: 'Image Version of the application')
    }
    stages{
        stage('Deployment'){
            steps{
                script{
                     withAWS(credentials: 'aws-cred', region: 'us-east-1') {
                        sh """
                           aws eks update-kubeconfig --region ${REGION} --name ${PROJECT}
                           kubectl get nodes
                           sed -i "s/IMAGE_VERSION/${params.appVersion}/g" values.yaml
                           helm upgrade --install ${COMPONENT} -f values.yaml .
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