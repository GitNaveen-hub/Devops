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
    	withSonarQubeEnv('sonarqube') {
     	 	sh 'mvn clean package sonar:sonar'
    		} // submitted SonarQube taskId is automatically attached to the pipeline context
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

