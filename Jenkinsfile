pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Chandrika1112/devops-project-3.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh '''
                echo "Workspace:"
                pwd
                ls -l
                echo "Index.html content:"
                cat index.html
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t chandrika2002/devops-project-3:latest .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                docker stop devops-project-3 || true
                docker rm devops-project-3 || true
                docker run -d -p 80:80 --name devops-project-3 chandrika2002/devops-project-3:latest
                '''
            }
        }
    }

    post {
        success {
            echo '✅ CI/CD completed successfully'
        }
        failure {
            echo '❌ CI/CD failed'
        }
    }
}
