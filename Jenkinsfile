pipeline {
  agent any
  environment {
    registryCredential = 'dockerhub'
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t mohsinejaz/test-node-app .'
     } 
   }
   stage('Test') {
      steps {
        sh 'docker container rm -f node || true'
        sh 'docker container run -p 8001:8080 --name node -d mohsinejaz/test-node-app'
	sh 'sleep 10'
        sh 'curl -I http://localhost:8001'
      } 
   }
    stage('Publish') {
        steps{
            script {
                docker.withRegistry( '', registryCredential ) {
		 sh 'docker push mohsinejaz/test-node-app:latest'
               } 
           }
        }       
    }
  }
}
