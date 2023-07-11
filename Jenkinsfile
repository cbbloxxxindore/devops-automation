pipeline {
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/cbbloxxxindore/devops-automation']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t javatechie/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhupwd', variable: 'dockerhubpwd')]) {
                   bat 'docker login -u abhijeetmishu -p ${dockerhubpwd}'

}
                   bat 'docker push javatechie/devops-integration'
                }
            }
        }
        
    }
}
