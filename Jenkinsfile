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
             }
            }
      stage('SonarQube analysis') {
  	//  def scannerHome = tool 'SonarScanner 4.0';
	     steps{
    		withSonarQubeEnv('sonarqube-8.9.3') { 
		// If you have configured more than one global server connection, you can specify its name
      		sh "mvn sonar:sonar"
	    	}
      		}
	  stage("deploy-dev"){
       		steps{
          	sshagent(['0f32a7cf-2c58-452b-8b03-b9cfb2f59207']) {
    			sh """ scp -o StrictHostKeyChecking=no target/*.war root@192.168.0.162:/opt/apache-tomcat-8.5.73/webapps/ 
			ssh root@192.168.0.162 /opt/apache-tomcat-8.5.73/bin/shutdown.sh
          		ssh root@192.168.0.162 /opt/apache-tomcat-8.5.73/bin/startup.sh
	  		"""
		  
		}
          }
        }
      }
    }
}
