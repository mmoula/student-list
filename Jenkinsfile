pipeline {
     environment {
       IMAGE_NAME = "student-api"
       IMAGE_TAG = "v1"
       IMAGE_REPO = "mmoula"
     }
     agent none
     stages {
         stage('Build image') {
             agent any
             steps {
                script {
                  sh 'cd simple_api && docker build -t $IMAGE_NAME:$IMAGE_TAG .'
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
                    curl http://172.17.0.1:80 | grep -q "error"
                '''
              }
           }
      }
      stage('Clean Container') {
          agent any
          steps {
             script {
               sh '''
                  docker rm -vf ${IMAGE_NAME}
               '''
             }
          }
     }
        stage('deploy with ansible') {
            agent { docker { image 'dirane/docker-ansible:latest' } }
            steps {
                script {
                    
                    sh '''
			cd ansible
                        ansible-playbook -i prod.yml install-docker.yml
			ansible-playbook -i prod.yml student.yml
			'''
                }
            }
        }

    }
}
