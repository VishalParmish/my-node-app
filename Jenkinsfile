pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar_token')  // Reference to Jenkins credential
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Pulls code from Git or other VCS
            }
        }

        stage('Build') {
            steps {
                echo 'Insert your build steps here'
                // sh 'mvn clean install' or 'npm install' etc.
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube1') {
                    sh '''
                       sonar-scanner \
                          -Dsonar.projectKey=my_project_key \
                          -Dsonar.projectName=my-node-app \
                          -Dsonar.sources=src \
                          -Dsonar.host.url=http://localhost:9000 \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}

