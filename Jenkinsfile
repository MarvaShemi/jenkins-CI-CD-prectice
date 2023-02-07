/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'python:3.10.7-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
        stage('Build image') {
            dockerImage = docker.build("jenkinsrealthing:latest .")
            }
        }
        stage('Push image') {
            withDockerRegistry ([ credentialsId: 341278251429, url: "https://github.com/MarvaShemi/jenkins-CI-CD-prectice.git" ]) {
                dockerImage.push()
                }
            }
    }
}
