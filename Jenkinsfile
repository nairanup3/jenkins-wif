pipeline {
    agent any
    stages {
       
stage ("creds"){steps { script {node {    
withCredentials([file(variable: 'ID_TOKEN_FILE', credentialsId: 'openid1')]) {
  writeFile file: "$WORKSPACE_TMP/creds.json", text: """
    {
      "type": "external_account",
      "audience": "//iam.googleapis.com/projects/461592450968/locations/global/workloadIdentityPools/test/providers/google",
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
    cat $ID_TOKEN_FILE
    gcloud auth login --brief --cred-file=$WORKSPACE_TMP/creds.json
    gcloud auth print-identity-token --audiences=//iam.googleapis.com/projects/461592450968/locations/global/workloadIdentityPools/test/providers/google
    gcloud container clusters list
  '''
}}}}}
    }    
}
