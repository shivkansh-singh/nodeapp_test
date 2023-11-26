pipeline {
    agent any
    stages {
        stage('Go to Git') {
            steps {
                checkout scm
            }
        }
        stage('Build and Push') {
            steps {
                script {
                    def dockerImage = "aryansr/nodejs-2"
                    def dockerTag = "v2"
                    def dockerCredentialsId = "dockerhub_credentials"

                    def dockerBuild = docker.build("${dockerImage}:${dockerTag}",".")
                    docker.withRegistry('', dockerCredentialsId) {
                        dockerBuild.push()
                    }
                }
            }
        }
    }
}
