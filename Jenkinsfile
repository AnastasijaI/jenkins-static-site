pipeline {
   agent any


   stages {
       stage('Build') {
           steps {
	       script {
	           dockerImage=docker.build("docker_hub/my-static-site:${env.BUILD_NUMBER}")	
               }	              
           }
       }

       stage('Push') {
           steps {
	       script {
                   docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-creds') {
		       dockerImage.push()
                   }	
               }
           }	
       }	
   }
}
