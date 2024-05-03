pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/rushikesh-rawool10/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPassword",usernameVariable:"DockerHubUser")]){
                    sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPassword}"
                     sh "docker tag node-app-test-new ${env.DockerHubUser}/node-app-new:latest"
                     sh "docker push ${env.DockerHubUser}/node-app-new:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
