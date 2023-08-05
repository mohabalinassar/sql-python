pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                // Build Docker image from the Dockerfile
                script {
                    docker.withRegistry('docker.io', 'DockerHub-Cred') {
                        def customImage = docker.build('docker.io/testjenkins:last', '.')
                        customImage.push()
                    }
                }
            }
        }

        stage('Deploy with docker-compose') {
            steps {
                // Run docker-compose to deploy the stack
                script {
                    sh "docker-compose up -d"
                }
            }
        }
    }
}
