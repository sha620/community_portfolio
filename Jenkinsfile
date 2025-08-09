pipeline{
    agent any;
    stages{
        stage("code clone from github"){
            steps{
                git url :"https://github.com/sha620/community_portfolio.git", branch:"main"
            }
            
        }
        stage("code build"){
            steps{
                sh "docker build -t node-app:latest ."
            }
        }
        stage("code test"){
            steps{
                echo "king"
            }
        }
        stage("code push to dockerhub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"Dockerhubcred",
                passwordVariable:"dockerhubpass",
                usernameVariable:"dockerhubuser"
                )]){
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                sh "docker image tag node-app:latest ${env.dockerhubuser}/node-app:latest"
                sh "docker push ${env.dockerhubuser}/node-app:latest"
                }
            }
        }
        stage("code deploy"){
         steps{
             sh "docker run -d -p 3000:3000 node-app:latest"
         }   
        }
    }
    
}
