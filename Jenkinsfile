#!/usr/bin/env groovy

pipeline{
    agent any
    tools {
        maven "maven"
    }
    stages{
        stage("build jar") {
            steps{
                script  {
                    echo "bulding the application"
                    sh "mvn package"
                }
            }
        }
        stage("build docker iamage") {
            steps{
                script  {
                    echo "bulding the docker image"
                    withCredentials([usernamePassword(credentialsId: 'dockerHub-Credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t faizalshikalgar/demo-app:jma-2.0 ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push faizalshikalgar/demo-app:jma-2.0"
                            
                    }
                }
            }
        }
        stage("deploy") {
            steps{
                script  {
                    echo "deploying the application"
                }
            }
        }
    }
}
