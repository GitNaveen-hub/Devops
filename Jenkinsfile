pipeline{
  agent any
  stages{
   stage("build & SonarQube analysis") {
          steps{
              withSonarQubeEnv('sonarqube') {
                 sh 'mvn clean package sonar:sonar'
              }
          }
      }   
   }
}

