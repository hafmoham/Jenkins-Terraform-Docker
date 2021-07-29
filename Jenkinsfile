properties([ parameters([
  string( name: 'AWS_ACCESS_KEY_ID', defaultValue: ''),
  string( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: ''),
  string( name: 'AWS_REGION', defaultValue: ''),
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
            sh "export TF_VAR_aws_region='${env.aws_region}' && export TF_VAR_indexer_count='${env.indexer_count}' && terraform plan" 
         }
      }
         stage ('Terraform Apply - Create Instances and Configurig Clustering'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && export TF_VAR_indexer_count='${env.indexer_count}' && terraform apply -auto-approve"
        }
      }
    }
  }
