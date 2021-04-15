pipeline {
  environment { 
        registry = "riderd758/pipelinetestprod" 
        registryCredential = 'dockerhub' 
        dockerImage = '' 

    }
    agent any
    stages {

        stage('Clone Repo') {
          steps {
            sh 'rm -rf DockerTest1'
            sh 'git clone https://github.com/sitaramchowdaryunnam/DockerTest1.git'
            }
        }

        stage('Build Docker Image') {
          steps {
          sh 'ls -al'
	  sh 'pwd'
          sh 'docker build -t riderd758/feauterwebapp3:${BUILD_NUMBER} .'
            }
        }

        stage('Push Image to Docker Hub') {
          steps {
           sh    'docker push riderd758/feauterwebapp3:${BUILD_NUMBER}'
           }
        }

        stage('Deploy to Docker Host') {
          steps {
            sh    'docker -H tcp://10.1.2.200:2375 stop feauterwebapp3 || true'
            sh    'docker -H tcp://10.1.2.200:2375 run --rm -dit --name feauterwebapp3 --hostname feauterwebapp3 -p 11000:80 riderd758/feauterwebapp2:${BUILD_NUMBER}'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'sleep 10s'
          sh ' curl http://10.1.2.200:11000'
          }
        }

    }
}
