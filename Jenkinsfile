pipeline {
  environment {
    registry = "11503542"
    registryCredential = 'docker'
    dockerImage = ''
  }
  agent an
  stages{
    tage('package'){
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
          docker.withRegistry( '', registryCredential ) {
              dockerImage.push()
              dockerImage.push('latest')
          }
        }
      }
    }
    stage ('Deploy to Dev') {
      steps{
        echo "Deploying to Dev Environment"
        sh "docker rm -f petclinic || true"
        sh "docker run -d --name=petclinic -p 8081:8080 prabhavagrawal/petclinic"
      }
    }
  }
}
