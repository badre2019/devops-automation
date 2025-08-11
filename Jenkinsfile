pipeline {
    agent any
    tools{
        maven "maven_3.9.11"
    }
    stages{
        stage("build maven"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/badre2019/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage("build docker image"){
            steps{
                script{
                    bat 'docker build -t bader20200/devops-integration .'
                }
            }
        }
        stage('push image to dockerHub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhuptoken', variable: 'dockerhub-pwd')]) {
                        bat 'docker login --username bader20200 -p "%dockerhub-pwd%"'
                    }
                    bat 'docker push bader20200/devops-integration'
                }
            }
        }
    }