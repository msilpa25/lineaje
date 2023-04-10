pipeline {
    agent any

    environment {
        GIT_BRANCH = "main"
        GIT_URL = "https://git-codecommit.ap-southeast-2.amazonaws.com/v1/repos/app-repo"
        GIT_CREDENTIALS_ID = "7ba34983-32a5-4a18-b1c7-ca3b81fa78ef"
    }

    stages {
        stage("Clone Git repository") {
            steps {
                git branch: "${GIT_BRANCH}",
                    credentialsId: "${GIT_CREDENTIALS_ID}",
                    url: "${GIT_URL}"
            }
        }
        stage("Build and Push to Docker Hub") {
             steps {
                  sh """#!/bin/bash
                    aws ecr get-login-password --region ap-southeast-2 |sudo docker login --username AWS --password-stdin 073515860795.dkr.ecr.ap-southeast-2.amazonaws.com
                    sudo docker build -t my-registry .
                    sudo docker tag my-registry:latest 073515860795.dkr.ecr.ap-southeast-2.amazonaws.com/my-registry:latest
                    sudo docker push 073515860795.dkr.ecr.ap-southeast-2.amazonaws.com/my-registry:latest
                  """
             }
         }
        }
    }
