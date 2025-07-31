pipeline {
    agent any

    environment {
        IMAGE_TAG = "latest"
    }

    stages {

            steps {
                git 'https://github.com/tvann00046/fintrack-project.git'
            }
        }

        stage('Code Analysis - SonarQube') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn -f backend/pom.xml clean verify sonar:sonar'
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
