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
     stage("deploy-docker"){
       steps{
          sh """
<<<<<<< HEAD
          docker container run -d -p --name ${env.JOB_NAME}-${BUILD_NUMBER} humayunalam/tomcat-maven
=======
          docker container run -d -p 8888:8080 --name ${env.JOB_NAME}-${BUILD_NUMBER} humayunalam/tomcat-maven
>>>>>>> 6f10abdd7a7f7ea921a52c91223d35a784f7e5d0
          docker cp target/*.war ${env.JOB_NAME}-${env.BUILD_NUMBER}:/opt/tomcat/webapps
          """
            }
          }
        }
      }
