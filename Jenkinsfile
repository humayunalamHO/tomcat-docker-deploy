pipeline{
  agent {
    label "test-server"
  }

  tools {
    maven "maven"
  }
  stages{
    stage("Git Checkout"){
      steps{
          git branch: 'main',
            credentialsId: 'github',
            url: 'https://github.com/humayun-alam/tomcat-docker-deploy.git'
           }
          }
     stage("Maven Build"){
       steps{
            sh "mvn clean package"
            sh "mv target/*.war target/myweb.war"
             }
            }
     stage("deploy-dev"){
       steps{
          sh "echo hello"
          sh "docker container run -d -p 8888:8080 --name tomcat_docker humayunalam/tomcat-maven"
          sh "docker cp target/*.war tomcat_docker:/opt/tomcat/webapps"
            }
          }
        }
      }
