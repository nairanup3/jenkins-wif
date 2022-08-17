pipeline {
    agent any
    stages {
       stage("Generating OIDC token and saving it to a file") {
            steps {
                script {
                       // sh (script: 'gcloud auth print-identity-token anup-repo@searce-playground-v1.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/512447805963/locations/global/workloadIdentityPools/test-jenkins/providers/jenkins"  > /usr/share/token/key',returnStdout: true)
                }
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                    script
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=/usr/share/token/clientLibraryConfig-aws-provider.json --quiet
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
