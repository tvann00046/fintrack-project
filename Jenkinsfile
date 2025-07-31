pipeline {
    agent any

    environment {
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Code Analysis - SonarQube') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker-compose build'
            }
        }

        stage('Deploy Local') {
            steps {
                bat 'docker-compose down'
                bat 'docker-compose up -d'
            }
        }
    }
}
