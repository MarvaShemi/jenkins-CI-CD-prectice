/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        stage('Build') {
            steps {
                script{
                    app = docker.build("coolpipeline")
                }
            }
        }
        stage('Test'){
            steps {
                echo 'Empty'
            }
        }
                stage('Deploy') {
            steps {
                script{
                    docker.withRegistry('http://341278251429.dkr.ecr.eu-west-1.amazonaws.com', 'ecr:eu-west-1:341278251429') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        stage('Pull') {
            steps {
                sh 'ssh ubuntu@3.251.71.232 "docker pull 341278251429.dkr.ecr.eu-west-1.amazonaws.com/jenkins-practice-pipeline1"'
                sh 'ssh ubuntu@3.251.71.232 "docker run 341278251429.dkr.ecr.eu-west-1.amazonaws.com/jenkins-practice-pipeline1"'
            }
        }
    }
}
