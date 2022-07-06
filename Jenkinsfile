pipeline {
    agent any
    environment {
        PROJECT_ID = 'anup-first-project'
        CLUSTER_NAME = 'cluster-1'
        LOCATION = 'us-central1'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("anupnairextras/hello:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com','docker-hub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
stage ("creds"){steps { script {node {    
withCredentials([file(variable: 'ID_TOKEN_FILE', credentialsId: 'openid1')]) {
  writeFile file: "$WORKSPACE_TMP/creds.json", text: """
    {
      "type": "external_account",
      "audience": "//iam.googleapis.com/projects/anup-first-project/locations/global/workloadIdentityPools/test/providers/static",
      "subject_token_type": "urn:ietf:params:oauth:token-type:jwt",
      "token_url": "https://sts.googleapis.com/v1/token",
      "service_account_impersonation_url": "https://iamcredentials.googleapis.com/v1/projects/-/serviceAccounts/jenkins-wif@anup-first-project.iam.gserviceaccount.com:generateAccessToken",
      "credential_source": {
        "file": "$ID_TOKEN_FILE",
        "format": {
          "type": "text"
        }
      }
    }
  """
  sh '''
    gcloud auth login --brief --cred-file=$WORKSPACE_TMP/creds.json
    gcloud container clusters list
  '''
}}}}}
    }    
}
