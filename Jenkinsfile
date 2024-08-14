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
                    def portInUse = sh(script: 'netstat -an | find \":8089\"', returnStatus: true) == 0
                    if (portInUse) {
                        echo 'Port 8089 is already in use. Stopping the existing service.'
                        def pid = sh(script: "netstat -an | find \":8089\" | awk '{print \$5}' | cut -d'/' -f1", returnStdout: true).trim()
                        sh "taskkill /F /PID ${pid}"
                    }
                    sh 'echo "Starting new Cloudflare tunnel..."'
                    sh 'cloudflared access ssh --hostname ssh-boi.nhungchangtrainhaycam.site --url 127.0.0.1:8089'
                }
            }
        }

        stage('ssh to server') {
            steps {
                sshagent(['boi-win-server-2019']) {
                    sh 'echo "ssh to server..."'
                    sh 'ssh -o "StrictHostKeyChecking=no" -p 8089 administrator@127.0.0.1 powershell.exe New-Item -Path C:\\Users\\Administrator\\test.txt -ItemType File'
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
