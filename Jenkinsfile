pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nisha1310/simple-demo:kubeimage1'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Starting Week 9 pipeline'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t kubdemoapp:v1 .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DH_USER',
                    passwordVariable: 'DH_PASS'
                )]) {
                    sh 'echo "$DH_PASS" | docker login -u "$DH_USER" --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker tag kubdemoapp:v1 nisha1310/simple-demo:kubeimage1'
                sh 'docker push nisha1310/simple-demo:kubeimage1'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment    l --validate=fal                sh 'kubectbe                vice.yaml'
            }
        }
    }

    post {    post {uccess {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
