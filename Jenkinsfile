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
          sh 'mvn sonar:sonar'
        }
      }
    }     
       
    }
}
