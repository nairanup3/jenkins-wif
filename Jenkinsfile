pipeline {
    agent any
    stages {
        stage ("getting the WIF config file into a variable")
        {
            steps {
                    script
                        {
                         sh '''
                         export 
                            gcloud auth login --brief --cred-file=/usr/share/token/clientLibraryConfig-aws-provider.json --quiet --project=searce-playground-v1
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
