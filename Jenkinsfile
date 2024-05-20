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
          //the jenkins user on the machine needs to be added to the docker group to avoid getting a permission denied error
          sh "docker build . -t tmorot/tutorial-frontend:v${env.BUILD_NUMBER}"
      
        }
      }
    }
    stage("Build backend docker image"){
      steps {
        dir('Tutorial-app/spring-boot-server'){
          //the jenkins user on the machine needs to be added to the docker group to avoid getting a permission denied error
          sh "docker build . -t tmorot/tutorial-backend:v${env.BUILD_NUMBER}"
      
        }
      }
    }
    stage("Push frontend and backend images to dockerhub"){
      steps {
      //the jenkins credentials binding plugin is required and you need to add your docker credentials to jenkins creds store
      withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'dockeruser', passwordVariable: 'dockerpass')]) {
        sh "docker login -u ${dockeruser} -p ${dockerpass}"
        sh "docker push tmorot/tutorial-frontend:v${env.BUILD_NUMBER}"
        sh "docker push tmorot/tutorial-backend:v${env.BUILD_NUMBER}"

}
    }
    }
  }
}
