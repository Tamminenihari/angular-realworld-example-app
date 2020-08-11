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
                    sh 'npm install'
               
                    }
            }
                stage('Build'){
                    steps{
                        sh 'ng serve --prod'  
                    }
                }
               


                
                   
	  
}
}
