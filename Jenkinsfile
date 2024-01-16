  pipeline {
      agent any
      stages {
          stage('Build') {
              steps {
		    sh ‘’’chmod +x scripts/build.sh
  scripts/build.sh’’’
              }
         }

          stage('Test') {
              steps {
		     sh ‘scrips/test.sh’
              }
         }

          stage('Build docker image') {
              steps {
		     sh ‘docker build -t adyger/practical_cicd_image .’
              }
         }

          stage('Push image to dockerhub') {
              steps {
                  script {
		       docker.withRegistry(‘https://registry.hub.docker.com’, ‘dockerhub-credentials’) {
				                  sh ‘docker push adyger/practical_cicd_test_image’
                  }
              }
          }
      }
  }
  environment {
       DOCKERHUB_CREDENTIALS = credentials (‘dockerhub-credentials’)
  }
}
