pipeline {
    environment {
        dockerimagename = "shivkanshsingh/nodeapp"
        dockerImage = ""
        registryCredentials = "dhub_creds"
    }
    agent any

    stages {
        stage("Checkout Git") {
            steps {
                git "https://github.com/shivkansh-singh/nodeapp_test.git"
            }
        }
        stage("Build Image") {
            steps {
                script {
                    dockerImage = docker.build dockerimagename
                }
            }
        }
        stage("Push Image") {
            steps {
                script {
                    docker.withRegistry("", registryCredentials) {
                        dockerImage.push("latest")
                    }
                }
            }
        }
        stage("Deploy to Kubernetes") {
            steps {
             withKubeConfig([credentialsId: 'k8s-creds-2', serverUrl: 'https://10.0.0.100:6443']) {
                sh "kubectl apply -f deploymentservice.yml"
             }
            }
        }
    }
}
