pipeline {
    agent any

    stages {
        stage('test') {
            steps {
                sh 'terraform -version'
            }
        }
         stage('aws') {
            steps {
                sh 'aws ec2 describe-instances --region us-east-1'
            }
            
        }
        stage('ansible') {
            steps {
                sh """
                /usr/local/bin/ansible --version
                """
            }
        }
         stage('download-ssh-key') {
            steps {
                sh """
                aws ssm get-parameters \
                    --output=text \
                    --region us-east-1 \
                    --with-decryption \
                    --names jenkins-agent-bootstrap-ssh-key \
                    --query "Parameters[*].{Value:Value}[0].Value" > private-key private-key
                chmod 0600 private-key
                """
            }
        }
        stage('ping-ansible-host') {
            steps {
                sh """
                cd dynamic_inventory 
                /usr/local/bin/ansible linux -m ping
                """
            }
        }
    }
}