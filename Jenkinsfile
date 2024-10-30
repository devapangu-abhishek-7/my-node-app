pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/<your-github-username>/my-node-app.git', branch: 'main'
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
