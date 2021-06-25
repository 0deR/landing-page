properties([pipelineTriggers([githubPush()])])
pipeline {
    agent { label 'master' }
      stages {
        stage("Clone Code") {
            steps {
                script {
                checkout scm
                }
            }
        }
        stage('Building Image') {
            steps{
                script {
                    sh "docker build . -t 0der/jenkins:${BUILD_NUMBER}"
                }
            }
        }
        stage('Push dockerhub') {
            steps{
                script {
                    sh "docker push 0der/jenkins:${BUILD_NUMBER}"
                }
            }
        }
        stage('deploy to cluster') {
            steps{
                script {
                    sh "kubectl  set image deployment/pesbuk pesbuk=0der/jenkins:${BUILD_NUMBER}"
                }
            }
        }  
     }
   }
