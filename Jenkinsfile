pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/devapangu-abhishek-7/my-node-app.git', 
                    branch: 'master', 
                    credentialsId: '88fb11e3-852a-4e50-9961-e909aac59248'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def app = docker.build("my-node-app:${env.BUILD_ID}")
                }
            }
        }
        stage('Run Tests') {
            steps {
                // Add your test commands here
                sh 'npm test' // Adjust this command based on your test setup
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.image("my-node-app:${env.BUILD_ID}").run('-p 3000:3000')
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deployment were successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
