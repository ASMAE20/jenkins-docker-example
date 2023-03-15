# jenkins-docker-example
# This is a Jenkins pipeline that I used for the project, which consists of two stages: Build Maven and Build Docker Image. The pipeline is executed on any available agent and utilizes the Maven tool. In the Build Maven stage, the code is checked out from a Git repository (using the scmGit plugin) and Maven is used to package the application. In the Build Docker Image stage, a Docker image is built using the Dockerfile in the application directory and tagged with 'asmaeel/my-app-1.0'. The code is written in Groovy and is organized into stages with clear steps and appropriate comments.
``````
pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitInfo', url:                                'https://github.com/ASMAE20/jenkins-docker-example.git']])
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

