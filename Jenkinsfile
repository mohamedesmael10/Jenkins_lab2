pipeline {
    agent any
    environment {
        DOCKER_IMAGE = " mohamedesmael/jenkins_lab1:${env.BUILD_NUMBER}"
        LATEST_IMAGE = "mohamedesmael/jenkins_lab1:latest"
        REGISTRY_CREDENTIALS = 'mohamedesmael_dockerhub'
        AWS_CREDENTIALS = 'aws-credentials-id'
        TERRAFORM_DIR = 'terraform'
        ANSIBLE_DIR = 'ansible'
    }
    stages {
       
        stage('Run Terraform') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: AWS_CREDENTIALS, accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    dir(TERRAFORM_DIR) {
                        sh '''
                            export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
                            export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
                            terraform init
                           # terraform destroy -auto-approve
                            terraform apply -auto-approve
                            chmod +x inventory.sh
                            ./inventory.sh
                        '''
                    }
                }
            }
        }
        stage('Run Ansible') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: AWS_CREDENTIALS, accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    dir(ANSIBLE_DIR) {
                        sh '''
                            cat inventory
                            ansible-playbook -i inventory react.yaml
                        '''
                    }
                }
            }
        }
    }
  
    post {
     always {
            // Clean up inventory file
            sh 'rm -f ansible/inventory'
        }
    }
}
