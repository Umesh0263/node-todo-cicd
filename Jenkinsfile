pipeline {
    agent any
    
    stages {
        
        stage("pull"){
            steps{
                git url: "https://github.com/Umesh0263/node-todo-cicd.git", branch: "master"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t nodetodoapp:latest ."
                echo 'code build bhi ho gaya'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerhub-pass",usernameVariable:"dockerhub-user")]){
                sh "docker login -u ${env.dockerhub-user} -p ${env.dockerhub-pass}"
                sh "docker tag nodetodoapp:latest ${env.dockerhub-user}/nodetodoapp1:latest"
                sh "docker push ${env.dockerhub-user}/nodetodoapp1:latest"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}
