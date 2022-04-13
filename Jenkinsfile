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
          // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean package sonar:sonar'
        }
      }
    }     
    }
       
    }
}
