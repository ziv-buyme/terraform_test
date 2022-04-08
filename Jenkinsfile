pipeline {
    agent none
    stages {
        stage('Build') {
            agent any
            steps {
                echo 'compiling...'
            }
        }
        stage('Init') {
            agent any
            tool name: 'Terraform', type: 'terraform'
            steps {
               sh 'terraform init'
               sh 'terraform plan'
            }
        }
        stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    def deploymentApproval = input message: 'Apply Terraform ?', ok: 'Apply', parameters: [booleanParam('Apply?')]
                }
            }
        }
        stage('Deploy') {
            agent any
            steps {
                echo deploymentApproval
            }
        }
    }
}
