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

        stage('Deploy') {
    steps {
        sshagent(['azure-vm-ssh']) {
            sh """
            ssh -o StrictHostKeyChecking=no azureuser@${SERVER_IP} '
                cd /home/azureuser/final-project/docker &&
                docker-compose down -v || true &&
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
