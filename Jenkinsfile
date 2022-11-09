pipeline {
    agent any
    tools{
        maven 'maven_3_8_6'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/theakshaywagh/edu-image-automation.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t theakshaywagh/edu-image-automation .'
                }
            }
        }
        stage('Push image to Dockerhub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u theakshaywagh -p ${dockerhubpwd}'

}
                   sh 'docker push theakshaywagh/edu-image-automation'
                }
            }
        }
        
    }
}
