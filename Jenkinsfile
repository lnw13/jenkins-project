pipeline {
    agent any

    stages {
        stage('lw - Build Docker Image') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/lnw13/jenkins-project']])
                script{
                    env.PATH = "/usr/local/bin:${env.PATH}"
                    sh 'docker build -t lnw13/lw-jenkins .'
                }
            }
            
        }
        stage('lw - Login to Dockerhub') {
            steps {
                script {
                    env.PATH = "/usr/local/bin:${env.PATH}"
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerpwd')]) {
                        sh 'docker login -u lnw13 -p ${dockerpwd}'
                    }
                }
            }
        }
        stage('lw - Push to Dockerhub') {
            steps {
                script {
                    env.PATH = "/usr/local/bin:${env.PATH}"
                    sh 'docker push lnw13/lw-jenkins'
                    
                }
            }
        }
    }
}

