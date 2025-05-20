pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/VishalParmish/my-node-app.git'
            }
        }
        environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    tools {
        // Add JDK or build tools if needed
        // jdk 'JDK11'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    sh """
                        sonar-scanner \
                          -Dsonar.projectKey=my_project_key \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=http://localhost:9000 \
                          -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }

        // Optional: Wait for quality gate result
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
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
