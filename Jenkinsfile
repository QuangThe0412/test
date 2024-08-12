pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/QuangThe0412/test.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'echo "Building..."'
            }
        }
        
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'echo "Deploying..."'
            }
        }
    }
}