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
          docker container run -d -P --name ${env.JOB_NAME}-${BUILD_NUMBER} humayunalam/tomcat-maven
          docker cp target/*.war ${env.JOB_NAME}-${env.BUILD_NUMBER}:/opt/tomcat/webapps
          echo "hellio thfjfjfjere"
	  """
            }
          }
        }
      }
