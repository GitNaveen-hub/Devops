pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'github', url: 'https://github.com/GitNaveen-hub/Devops.git'
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
          sshagent(['tomcat-dev1']) {
          sh """
          scp -o StrictHostKeyChecking=no target/myweb.war  
          fis001s@192.168.0.162 /opt/apache-tomcat-8.5.73/webapps/
          ssh fis001s@192.168.0.162 /opt/apache-tomcat-8.5.73/bin/shutdown.sh
          ssh fis001s@192.168.0.162 /opt/apache-tomcat-8.5.73/bin/startup.sh
           """
            }
          }
        }
      }
    }
	
