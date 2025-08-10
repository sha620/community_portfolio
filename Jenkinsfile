pipeline {
    agent {label "test"};
    stages{
        stage('code clone'){
            steps{
                git url : "https://github.com/sha620/community_portfolio.git", branch:"main"
            }
        }
        stage('code buil'){
          steps{
              sh "docker build -t noda-app:la ."
          }  
        }
        stage('code test'){
         steps{
             echo "test"
         }   
        }
        stage('code push to doker'){
            steps{
               withCredentials([usernamePassword(
               credentialsId: "key",
               usernameVariable: "user",
               passwordVariable: "pass"
               )]){
                   sh "docker login -u ${env.user} -p ${env.pass}"
                   sh "docker image tag noda-app:la ${env.user}/noda-app:la "
                   sh "docker push ${env.user}/noda-app:la"
               }
            }
        
        }
        stage('deploy'){
          steps{
              sh "docker stop noda && docker rm noda"
              sh "docker run -d --name noda -p 3000:3000 noda-app:la"
          }  
        }
    }
}
