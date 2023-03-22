pipeline {
    agent any
    parameters {
        string(name: 'playbook_name', defaultValue: 'ping_playbook.yaml', description: 'playbook name')
    }
    stages {
        stage('test') {
            steps {
                sh 'terraform -version'
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
                mv private-key dynamic_inventory 
                cd dynamic_inventory && pwd && ls -al
                """
                ansiblePlaybook installation: 'ansible', playbook: 'ping_playbook.yaml'
            }
        }
    }
}