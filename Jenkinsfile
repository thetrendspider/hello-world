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
        expression { currentBuild.changeSets.any { it.branch == 'origin/main' } && currentBuild.changeSets.any { it.originObject instanceof hudson.model.ChangeLogSet$Entry } }
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
