properties([ parameters([
  string( name: 'AWS_ACCESS_KEY_ID', defaultValue: ''),
  string( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: ''),
  string( name: 'AWS_REGION', defaultValue: 'us-east-1'),
]), pipelineTriggers([]) ])

// Environment Variables.
env.access_key = AWS_ACCESS_KEY_ID
env.secret_key = AWS_SECRET_ACCESS_KEY
env.aws_region = AWS_REGION


pipeline {
    agent any
   environment {
    PATH = "${PATH}:${getTerraformPath()}"
  }
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
def getTerraformPath(){
  def tfHome = tool name: 'terraform-12', type: 'org.jenkinsci.plugins.terraform.TerraformInstallation'
  return tfHome
}
