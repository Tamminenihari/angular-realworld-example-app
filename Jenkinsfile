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
                         npm install
                     '''
                    }
            }  
    stage ('Build') {
      steps{
        echo "Building Project"
        sh '''
                            npm run ng -- build --prod  
                        '''
      }
    }
    
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
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
