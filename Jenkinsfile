pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Use the Docker Pipeline plugin to build the Docker image
                    docker.image('your-docker-image-name').build()
                }
            }
        }

        stage('Push to ECR') {
            environment {
                // Set your AWS ECR repository URL and credentials
                ECR_REPO_URL = 'your-ecr-repo-url'
            }
            steps {
                script {
                    // Use the AWS ECR plugin to push the Docker image to ECR
                    docker.withRegistry(ECR_REPO_URL, 'ecr:us-east-1') {
                        docker.image('your-docker-image-name').push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            environment {
                // Set your Kubernetes configurations and credentials
                KUBECONFIG = credentials('your-kubeconfig')
            }
            steps {
                script {
                    // Use kubectl to apply the Kubernetes deployment
                    sh "kubectl apply -f your-kubernetes-deployment.yaml --kubeconfig=\${KUBECONFIG}"
                }
            }
        }
    }

    // Post-build actions, if needed
    post {
        // You can add cleanup or notifications here
    }
}
