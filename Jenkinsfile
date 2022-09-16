#!/usr/bin/env groovy
pipeline {
    agent any
    environment{
        VERSION = "${env.BUILD_ID"}"
    }
    stages {
        stage('Build Image') {
            when {
                branch 'master'  //only run these steps on the master branch
            }

            // Jenkins Stage to Build the Docker Image
            script{
                        sh 'docker build -t <nexus-server-ip:nexus-HTTP port>/flaskgapp:${VERSION} .'
                    }

        }

        stage('Publish Image') {
            when {
                branch 'master'  //only run these steps on the master branch
            }
            
            // Jenkins Stage to Publish the Docker Image to Dockerhub or any Docker repository of your choice.
            withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_password')]) {
                sh '''
                   docker login -u <nexus-username> -p $docker_password <nexus-server-ip:nexus-HTTP port> 
                   docker push  <nexus-server-ip:nexus-HTTP port>/flaskgapp:${VERSION}
                   docker rmi <nexus-server-ip:nexus-HTTP port>/flaskgapp:${VERSION}
                '''

        }
    }
}