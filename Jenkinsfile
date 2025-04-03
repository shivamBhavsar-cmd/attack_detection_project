// Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Fetch the repository directly from GitHub
                git url: 'https://github.com/shivamBhavsar-cmd/attack_detection_project.git', branch: 'main'
            }
        }

        stage('Run SSH Attack Detection') {
            steps {
                sh 'python3 ssh_attack_detection.py > ssh_result.txt'
            }
        }

        stage('Run DDoS Attack Detection') {
            steps {
                sh 'python3 ddos_attack_detection.py > ddos_result.txt'
            }
        }

        stage('Display Results') {
            steps {
                echo "=== SSH Attack Detection Result ==="
                sh 'cat ssh_result.txt'
                echo "=== DDoS Attack Detection Result ==="
                sh 'cat ddos_result.txt'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'ssh_result.txt, ddos_result.txt', allowEmptyArchive: true
            cleanWs()
        }
    }
}