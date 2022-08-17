pipeline {
    agent any
    stages {
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
