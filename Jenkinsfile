pipeline{
  agent any
  stages{
      stage("build") {
          steps{
               sh 'mvn clean package'
            }
        }
        stage("upload the war to nexus") {
          steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'deployment-project', 
                        classifier: '', 
                        file: 'target/deployment-project.war', 
                        type: 'war']
                        ], 
                        credentialsId: 'nexus3', 
                        roupId: 'com.deployment.project', 
                        nexusUrl: '172.31.23.60:8081', 
                        nexusVersion: 'nexus', 
                        protocol: 'http', 
                        repository: 'deployment-project', 
                        version: '1.1-SNAPSHOT'
            }
        }
   }   
}
