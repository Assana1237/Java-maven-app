pipeline {
    agent any
tools {
        maven 'maven-3.9'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t java-maven-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d --name test-app -p 8080:8080 java-maven-app'
            }
        }
    }
}
