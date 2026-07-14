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

        stage("build image") {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'DockerHub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t assana/demo-app:1.1 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push assana/demo-app:1.1'
                    }
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    echo "deploying the application..."
                }
            }
        }
    }
}
