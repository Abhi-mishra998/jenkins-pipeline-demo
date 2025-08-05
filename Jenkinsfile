pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'docker build -t my-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing the app...'
                // You can add test scripts here
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the app...'
                sh 'docker run -d --name my-app-container -p 3000:3000 my-app || true'
            }
        }
    }
}

