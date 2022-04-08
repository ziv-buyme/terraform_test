pipeline {
    agent any
    stages {
        stage('Build') {
            agent any
            steps {
                echo 'compiling...'
            }
        }
        stage('Init') {
            agent any
            steps {
               sh 'terraform init -no-color'
               sh 'terraform plan -no-color'
            }
        }
        stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    def deploymentApproval = input message: 'Apply Terraform ?', ok: 'Apply'
                }
            }
        }
        stage('Deploy') {
            agent any
            steps {
                sh 'ls -la'
            }
        }
    }
}
