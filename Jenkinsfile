pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_password')
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
                sh "docker build -t himimage1:latest ."
                sh 'docker tag himimage1 himanshudabhade/jenkinsmade:latest'
                sh 'docker tag himimage1 himanshudabhade/jenkinsmade:$BUILD_NUMBER'
            }
        }

        stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub_password", url: "" ]) {
          sh  'docker push himanshudabhade/jenkinsmade:latest'
          sh  'docker push himanshudabhade/jenkinsmade:$BUILD_NUMBER' 
        }
                  
          }
        stage('Run Docker container on Jenkins Server') {
             
            steps {
                sh "docker run -d -p 4030:8080 himanshudabhade/jenkinsmade"
 
            }
        }  
        }

    }
}
