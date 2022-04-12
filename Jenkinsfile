pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('originalDockerhubpassword')
  }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build . -t himimage1:latest"
            }
        }

        stage('Push') {
      steps {
        sh 'docker push himimage1:latest'
      }
    }

    }
}
