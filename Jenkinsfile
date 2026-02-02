pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t webapp:${BUILD_NUMBER} .'
            }
        }

        stage('Load Image into Minikube') {
            steps {
                sh 'minikube image load webapp:${BUILD_NUMBER}'
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh 'ansible-playbook ansible/deploy.yml -i ansible/inventory.ini'
            }
        }
    }
}
