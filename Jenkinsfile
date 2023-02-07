/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'python:3.10.7-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
        stage('build') {
            steps {
                sh 'docker build -t jenkinsrealthing:latest .'
            }
        } 
        stage('push') {
            steps {
                sh 'push DockerFile'
            }
        }
        stage('connect to ec2') {
            steps {
                sh 'check how to connect it'
            }
        }
    }
}
