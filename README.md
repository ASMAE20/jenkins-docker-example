# jenkins-docker-example
#this the pipeline code that i used

pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitInfo', url: 'https://github.com/ASMAE20/jenkins-docker-example.git']])
                sh 'mvn package'
             }    
                
        }
            
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t asmaeel/my-app-1.0 .'
                }
            }
        }
        
        
    }
}
