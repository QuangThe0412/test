pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/QuangThe0412/test.git'
            }
        }
        
        stage('Run clouflear tunnel') {
            steps {
                sh 'echo "clouflear tunnel..."'
                sh 'cloudflared access ssh --hostname ssh-boi.nhungchangtrainhaycam.site --url 127.0.0.1:8089'
            }
        }

        stage('ssh to server') {
            steps {
                sh 'echo "ssh to server..."'
                sh 'ssh -o "StrictHostKeyChecking=no" administrator@127.0.0.1 -p 8089'
            }
        }
        
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
            }
        }
    }
}