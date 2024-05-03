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
                sh "docker build . -t node-app-test-new-v2"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"DockerHubPassword",usernameVariable:"DockerHubUser")]){
                    sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPassword}"
                     sh "docker tag node-app-test-new-v2 ${env.DockerHubUser}/node-app-new:latest-v2"
                     sh "docker push ${env.DockerHubUser}/node-app-new:latest-v2" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker run -d -p 8000:8000 rushidevops10/node-app-new:latest-v2"
            }
        }
    }
}
