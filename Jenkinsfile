pipeline {
  agent any
options { 
  skipDefaultCheckout() 
}
  stages{
    stage("Clone source code repo"){
      steps {
      sh 'git clone https://github.com/Amr-tmorot/Tutorial-app.git'
      }
    }
    stage("Build frontend docker image"){
      steps {
        dir('Tutorial-app/angular-15-client'){
          sh "docker build . -t tmorot/tutorial-frontend:v${env.BUILD_NUMBER}"
        }
      }
    }
  }
}
