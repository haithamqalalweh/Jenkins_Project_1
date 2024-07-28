pipeline {
  environment {
    registry = "haithamqalalweh/project1"
    imagename = "web-app"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/haithamqalalweh/Jenkins_Project_1.git', branch: 'main', credentialsId: 'git-hub'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + "$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}
