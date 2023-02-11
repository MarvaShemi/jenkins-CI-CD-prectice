/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="341278251429"
        AWS_DEFAULT_REGION="eu-west-1"
        IMAGE_REPO_NAME="coolpipeline"
        IMAGE_TAG="v1"
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
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
