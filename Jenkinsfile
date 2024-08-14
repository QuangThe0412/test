pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/QuangThe0412/test.git'
            }
        }

        stage('Run cloudflare tunnel') {
            steps {
                script {
                    def portInUse = sh(script: 'netstat -an | grep ":8089"', returnStatus: true) == 0
                    if (portInUse) {
                        echo 'Port 8089 is already in use. Stopping the existing service.'
                    } else {
                        sh 'echo "Starting new Cloudflare tunnel..."'
                        sh 'cloudflared access ssh --hostname ssh-boi.nhungchangtrainhaycam.site --url 127.0.0.1:8089'
                    }
                }
            }
        }

        stage('ssh to server') {
            steps {
                sshagent(['boi-win-server-2019']) {
                    sh 'echo "ssh to server..."'
                    sh 'ssh -o "StrictHostKeyChecking=no" -p 8089 administrator@127.0.0.1 powershell.exe New-Item -Path C:\\Users\\Administrator\\test123.txt -ItemType File'
                }
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
            }
        }
    }
}
