pipeline {
     environment {
       IMAGE_NAME = "student-api"
       IMAGE_TAG = "latest"
       STAGING = "joris-staging"
       PRODUCTION = "joris-production"
       IMAGE_REPO = "joriscommin"
     }
     agent none
     stages {
         stage('Build image') {
             agent any
             steps {
                script {
                  sh 'docker build -t $IMAGE_REPO/$IMAGE_NAME:$IMAGE_TAG .'
                }
             }
        }
        stage('Run container based on builded image') {
            agent any
            steps {
               script {
                 sh '''
                    docker run --name $IMAGE_NAME -d -p 80:5000 $IMAGE_REPO/$IMAGE_NAME:$IMAGE_TAG
                    sleep 5
                 '''
               }
            }
       }
       stage('Test image') {
           agent any
           steps {
              script {
                sh '''
                    curl http://172.17.0.1:50 | grep -q "student"
                '''
              }
           }
      }
   }
}
