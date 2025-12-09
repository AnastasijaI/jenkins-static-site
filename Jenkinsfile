pipeline {
   agent any


   stages {
       stage('Build') {
           steps {
	       script {
	           dockerImage=docker.build("anastasijail/my-static-site:${env.BUILD_NUMBER}")	
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
       
       stage('Deploy to Prod') {
           steps {
               sshagent(['prod-ssh-key']) {
                   sh """
                   ssh -o StrictHostKEyChecking=no payten@192.168.229.128 '
                       docker pull anastasijail/my-static-site:${BUILD_NUMBER} &&
                       docker stop static_site || true &&
                       docker rm static_site || true &&
                       docker run -d --name static_site -p 8080:80 anastasijail/my-static-site:${BUILD_NUMBER}
                   '
                   """
               }
           }
       }	
   }
}
