#!groovy
pipeline {
    environment {
        registry = "sushmitasush/demo-evng-batch-eleven"
        registryCredentials = 'docker-credentials'
    }
    agent any
    stages {
        stage('Clone the Git Repository') {
            steps {
                git credentialsId: 'git-credentials', url: 'https://github.com/Susmitha890/rps-ant-testsush.git'
            }
        }
        stage('Building docker image') {
            steps {
                sh 'echo Building docker image'
                script {
                    buildDate = new Date()
                    image = docker.build("${registry}:$BUILD_NUMBER")
                }
            }
        }
        stage('Registry-Push') {
            steps {
                sh 'echo Registry-push'
                script {
                    docker.withRegistry('', registryCredentials) {
                        image.push()
                        image.push('latest')
                    }
                }
            }
        }
        stage('CleanUp workspace') {
            steps {
                sh ' echo CleanUp'
                sh "docker rmi ${registry}:${BUILD_NUMBER}"
            }
        }
    }
}
