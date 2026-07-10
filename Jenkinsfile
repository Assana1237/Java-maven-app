pipeline {
    agent any
tools {
        maven 'maven-3.9'
    }
    stages {
        stage('Checkout') {
            steps {
               echo 'checking out from https://github.com/Assana1237/Java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Running the Maven Build'
                sh 'mvn clean install'
            }
        }

         stage('Test') {
            steps {
                echo 'Unit test already run as part of the Maven build'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building the docker image java-maven-app:1.1'
                sh 'docker build -t java-maven-app:1.1 .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the Docker container to test environment'
                sh 'docker run -d --name test-app -p 8080:8080 java-maven-app:1.1'
            }
        }
    }
}
