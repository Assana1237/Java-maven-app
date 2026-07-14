pipeline {
    agent any
tools {
        maven 'maven-3.9'
    }
    stages {
        stage('Checkout') {
            steps {
               echo 'checking out source code from Github'
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Running the Maven Build and Unit tests'
                sh 'mvn clean install'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building the docker image demo-app:1.1'
                sh 'docker build -t demo-app:1.1 .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the Docker container to test environment'
                sh '''
        docker stop demo-app || true
        docker rm demo-app || true
        docker run -d \
          --name demo-app-test \
          -p 8080:8080 \
          demo-app:1.1
        '''
            }
        }
    }
}
