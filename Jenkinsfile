pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-app-image .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run my-app-image python -m unittest'
            }
        }
        stage('Deploy') {
            steps {
                // Deployment steps will be added later
            }
        }
    }
}
