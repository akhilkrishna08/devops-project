stage('Deploy') {
    steps {
        sshagent(['azure-vm-ssh']) {
            sh """
            ssh -o StrictHostKeyChecking=no azureuser@${SERVER_IP} '
                cd /home/azureuser/final-project/docker &&
                docker-compose down || true &&
                docker-compose pull &&
                docker-compose up -d
            '
            """
        }
    }
}
