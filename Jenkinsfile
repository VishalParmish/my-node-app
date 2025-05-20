pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "No tests defined."'
            }
        }

        stage('Build') {
            steps {
                echo 'Build step (placeholder)'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy step (manual or script-based)'
            }
        }
    }
}
