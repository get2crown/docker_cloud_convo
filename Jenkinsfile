pipeline {
  agent any

  environment {
       imagename = "hameedtech22/julyjavaimage:v3"
       registryCredential = 'Docker-hub'
       dockerImage = ''
           }

  
  stages {

    stage ('Build') {
      steps {
        sh 'mvn clean package'
        echo 'Maven Build'
      }
    }

    stage('Build Test') {
            steps {
                sh 'mvn test'
                echo 'Test Analysis'
            }
        }
    
      stage('Build Docker image') { 
          steps{
                script {
                   dockerImage = docker.build + ":$BUILD_NUMBER"
                          }
                      }
                }

     stage('Push Docker Image to DockerHub') {
           steps{
               script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                                              }
                                    }
                             }
                  }
     stage('Remove Unused docker image') {
          steps{
              sh "docker rmi $imagename:$BUILD_NUMBER"
                        }
            }  
   }
}
