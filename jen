pipeline {
    agent any
    
    stages {
        stage('checkout') {
            steps {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/arshavardan/task_tamasha.git']])
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "sudo docker build -t nodeimage:v1 ."
            }
        }
        stage('pushing Docker Image') {
            steps {
                sh "sudo docker tag nodeimage:v1 arshavardan/nodeimage:v1"
                sh "sudo docker push arshavardan/nodeimage:v1"
            }    
        }
        stage("deploy to k8s") {
            steps {
                kubernetesDeploy(
                configs: "deploysvc.yaml",
                kubeconfigId: "k8sdeploy",
                )
            }
        } 
    } 
}
