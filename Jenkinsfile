pipeline {
   agent any


   stages {
       stage('Build Docker Image') {
           steps {
	       script {
	           docker.build("my-static-site:${env.BUILD_NUMBER}")	
               }	              
           }
       }
   }
}
