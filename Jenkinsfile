pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/maven/bin"
    }
    stages{        
       stage('Build'){
            steps{
                sh 'mvn clean package'
            }
         }

        stage('Scan') {
            steps {
        withSonarQubeEnv(installationName: 'sonarqube') { 
          sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
        }
      }
    }     
       
    }
}
