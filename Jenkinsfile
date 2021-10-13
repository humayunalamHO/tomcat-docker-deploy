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
     stage("deploy-dockerfile"){
       steps{
          sh """
          docker build -t humayunalam/tomcat_dockerfile:${env.BUILD_ID} .
	  docker tag humayunalam/tomcat_dockerfile:${env.BUILD_ID} humayunalam/tomcat_dockerfile:latest
          docker container run -d -P --name dockerfile-${env.BUILD_NUMBER} humayunalam/tomcat_dockerfile:${env.BUILD_ID}
          docker cp target/*.war dockerfile-${env.BUILD_NUMBER}:/opt/tomcat/webapps
          """
            }
          }
        }
        post {
              success {
                 withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    sh "docker push humayunalam/tomcat_dockerfile:${env.BUILD_ID}"
                    sh "docker push humayunalam/tomcat_dockerfile:latest"
                } 
             }
         }
    }
