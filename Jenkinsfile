/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stage('Cloning Git') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/MarvaShemi/jenkins-CI-CD-prectice.git']])     
            }
        }
    stages {
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
    }
}
