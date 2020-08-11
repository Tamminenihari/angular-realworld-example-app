pipeline {
  environment {
    registry = "11503542"
    registryCredential = 'docker'
    dockerImage = ''
  }
  agent any
  stages{
    stage('package'){
                steps{
                    sh '''
                         yarn install
                     '''
                    }
            }  
    stage ('Build') {
      steps{
        echo "Building Project"
        sh '''
                          ng serve --prod  
                        '''
      }
    }
    
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
        script {
          dockerImage = docker.build angular-realworld-example-app + ":$BUILD_NUMBER"
        }
      }
    }
    stage ('Push Docker Image') {
      steps{
        echo "Pushing Docker Image"
        script {
          withDockerRegistry(credentialsId: 'registryCredential') {
             dockerImage.push()
              dockerImage.push('latest')
    
             }
        }
      }
    }
    
  }
}
