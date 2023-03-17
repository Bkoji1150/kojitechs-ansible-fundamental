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
    }
}