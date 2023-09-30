properties([ parameters([
  string( name: 'AWS_ACCESS_KEY_ID', defaultValue: 'AKIASBGHG4TTNBEXDSMF'),
  string( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: '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'),
  string( name: 'AWS_REGION', defaultValue: 'us-east-1'),
]), pipelineTriggers([]) ])

// Environment Variables.
env.access_key = AWS_ACCESS_KEY_ID
env.secret_key = AWS_SECRET_ACCESS_KEY
env.aws_region = AWS_REGION


pipeline {
    agent any
    stages {
         stage ('Terraform Init'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && terraform init"
          }
       }
         stage ('Terraform Plan'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && terraform plan" 
         }
      }
         stage ('Terraform Apply & Deploy Docker Image on Webserver'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && terraform apply -auto-approve"
        }
      }
    }
  }
