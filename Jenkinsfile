pipeline {
  agent any
options { 
  skipDefaultCheckout() 
}
  stages{
    stage("Clone source code repo"){
      steps {
      cleanWs()  //cleaning workspace before cloning, this step requires installing the Workspace cleanup plugin
      sh 'git clone https://github.com/Amr-tmorot/Tutorial-app.git'
      }
    }
    stage("Build frontend docker image"){
      steps {
        dir('Tutorial-app/angular-15-client'){
          sh "sudo docker build . -t tmorot/tutorial-frontend:v${env.BUILD_NUMBER}"
        }
      }
    }
  }
}
