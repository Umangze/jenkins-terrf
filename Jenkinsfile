pipeline {
    agent any
    stages {
        stage("Generating OIDC token and saving it in a file") {
            steps {
                script {
                    sh (script: 'gcloud auth print-identity-token gcp-jenkinsvm-sa@western-passkey-436609-b4.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/594929244584/locations/global/workloadIdentityPools/jenkinspool/providers/jenkins"  > /usr/share/token/key',returnStdout: true)
                }
            }
        }
        stage("Getting the config file into variable") {
          steps {
               withCredentials([file(credentialsID: 'wif-config-file', variable: 'WIF')])
               {
                sh '''
                   gcloud auth login --brief --cred-file=$WIF --quiet
                   gcloud compute instances list
                '''
               }
          }
        }
    }
}