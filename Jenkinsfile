pipeline {
    agent any

    environment {
        IMAGE_NAME = "chandrika2002/devops-project-3"
        KUBECONFIG = "/etc/rancher/k3s/k3s.yaml"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Chandrika1112/devops-project-3.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([string(credentialsId: "dockerhub-password", variable: "PASS")]) {
                    sh 'echo $PASS | docker login -u chandrika2002 --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }

        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful"
        }
        failure {
            echo "❌ Deployment Failed"
        }
    }
}
