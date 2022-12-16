pipeline {
    agent any
    tools{
       maven:3.8.1-adoptopenjdk-11
       
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/LoukHich/Docker-Jenkins-Pipeline.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t nadori/devops-integration-pip .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u nadori -p ${dockerhubpwd}'

}
                   sh 'docker push nadori/devops-integration'
                }
            }
        }

    }
}
