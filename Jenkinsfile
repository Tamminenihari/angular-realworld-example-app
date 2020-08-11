pipeline {
   agent any
   tools {
		nodejs 'nodejs'
        
            }
   stages {
       stage('Git-Checkout') {
         steps {
            git 'https://github.com/Tamminenihari/angular-realworld-example-app.git'
         }
      }
	   stage('npm install package'){
                steps{
                    sh label: '', script: '''
                        yarn install
                         npm install
                         
                     '''
                    }
            }
                stage('Build'){
                    steps{
                        sh 'ng build --prod'  
                    }
                }
                stage(' docker Build'){
                    steps{
                        sh 'ng build --prod'
                        sh 'docker build -t angular-realworld-example-app .'  
                        sh 'docker run --rm -d  -p 80:80/tcp angular-realworld-example-app:latest'
                    }
                }

                stage(' docker Build'){
                    steps{
                        
                    }
                }


                
                   
	  
}
}