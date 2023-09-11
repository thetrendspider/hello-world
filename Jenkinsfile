pipeline {
    agent any
    stages {
        
        stage('Welcome to testing') {
            steps {
                
                    echo 'welcome to testing'
                
            }
        }
        stage('Terraform Init') {
            steps {
                
                    echo 'terraform init'
                
            }
        }

        stage('Terraform Plan') {
            when {
                // Only run this stage on pull requests targeting the master branch
                expression { currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause) == null }
            }
            steps {
                
                    echo 'terraform plan'
               
            }
        }

        stage('Terraform Apply') {
            when {
                // Only run this stage when changes are merged into the master branch
                expression { currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause) != null }
            }
            steps {
                
                    echo 'terraform apply -auto-approve'
                
            }
        }
    }
}
