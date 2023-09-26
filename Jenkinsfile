pipeline {
    agent any
        stages{
        stage("Git Clone"){
            steps{
                git url: "https://github.com/kshitijabartakke/calculategrowth.git", branch: "main"
            }
        }
        stage("Create Docker Image"){
            steps{
                echo "Build and Test"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker build -t ramjanaki15/calculategrowth ."
                    }
            }
        }
         stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker images"
                    sh "docker push ramjanaki15/calculategrowth:latest"
                }
            }
        }
        stage("Deploy Using DOcker Compose"){
            steps{   
                 sh "docker ps"           
                }
            }
        }
    }
