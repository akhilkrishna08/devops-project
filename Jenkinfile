pipeline {
    agent any

    stages {

        stage('Pull from GitHub') {
            steps {
                git branch: 'main',
                url: 'https://github.com/akhilkrishna08/devops-project.git'
            }
        }

        stage('Deploy Docker Compose') {
            steps {
                sh '''
                cd $WORKSPACE
                docker-compose down || true
                docker-compose pull
                docker-compose up -d
                '''
            }
        }

        stage('Post-build Message') {
            steps {
                echo "Deployment Successful!"
            }
        }
    }
}
