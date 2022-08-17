pipeline {
    agent any
    stages {
        stage ("getting the WIF config file into a variable")
        {
            steps {
                    script
                        {
                         sh '''
                            /home/ubuntu/google-cloud-sdk/bin/gcloud auth login --brief --cred-file=/usr/share/token/clientLibraryConfig-aws-provider.json --quiet
                            /home/ubuntu/google-cloud-sdk/bin/gcloud container clusters list
                            /home/ubuntu/google-cloud-sdk/bin/gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
