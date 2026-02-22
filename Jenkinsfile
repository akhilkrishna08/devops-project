pipeline {
    agent any

    environment {
        SERVER_IP = "104.211.55.89"
    }

    stages {

        stage('Pull Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Azure VM') {
            steps {
                sshagent(['azure-vm-ssh']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no azureuser@${104.211.55.89} '
                        cd /home/azureuser/docker-compose.yml &&
                        docker-compose down || true &&
                        docker-compose up -d
                    '
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
