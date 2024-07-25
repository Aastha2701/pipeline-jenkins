pipeline {
    agent any

    stages{
        stage("code from github"){
            steps {
                echo "code aagaya repo se"
                git url: "https://github.com/urdevopswithdev/pipeline-jenkins.git", branch: "master"
            }
        }
        stage("now build code"){
            steps {
                echo "code build v hogya h"
                sh "docker build . -t mypipelineimg:latest"
            }
        }
        stage("code test"){
            steps {
                echo "code testing hogya"
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag mypipelineimg ${env.dockerHubUser}/mypipelineimg:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/mypipelineimg:latest"
                }
            }
        }
        stage("deploy"){
            steps {
                echo "deploying container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
