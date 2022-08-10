pipeline {
    agent any
    stages {
       
stage ("creds"){steps { script {node {    
withCredentials([file(variable: 'ID_TOKEN_FILE', credentialsId: 'oidc1')]) {
  writeFile file: "$WORKSPACE_TMP/creds.json", text: """
    {
      "type": "external_account",
      "audience": "//iam.googleapis.com/projects/512447805963/locations/global/workloadIdentityPools/test-jenkins/providers/jenkins",
      "subject_token_type": "urn:ietf:params:oauth:token-type:jwt",
      "token_url": "https://sts.googleapis.com/v1/token",
      "service_account_impersonation_url": "https://iamcredentials.googleapis.com/v1/projects/-/serviceAccounts/jenkin-wif@searce-playground-v1.iam.gserviceaccount.com:generateAccessToken",
      "credential_source": {
        "file": "$ID_TOKEN_FILE",
        "format": {
          "type": "text"
        }
      }
    }
  """
  sh '''
    cat $ID_TOKEN_FILE
    gcloud auth login --brief --cred-file=$WORKSPACE_TMP/creds.json
    gcloud container clusters list
  '''
}}}}}
    }    
}
