pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                echo 'Building Java application...'
                bat 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t sample-app:latest .'
            }
        }

        stage('Docker Run') {
            steps {
                echo 'Running Docker container...'
                bat 'docker stop sample-container 2>NUL || exit 0'
                bat 'docker rm sample-container 2>NUL || exit 0'
                bat 'docker run -d --name sample-container sample-app:latest'
            }
        }
    }

    post {
        success {
            echo 'CD Pipeline completed successfully!'
        }
        failure {
            echo 'CD Pipeline failed.'
        }
    }
}
