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
                sh "docker build . -t node-app-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPassword",usernameVariable:"DockerHubUser")]){
                    sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPassword}"
                     sh "docker tag node-app-new:latest ${env.DockerHubUser}/node-app-new:latest"
                     sh "docker push ${env.DockerHubUser}/node-app-new:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker run -d -p 8000:8000 rushidevops10/node-app-new"
            }
        }
    }
}
