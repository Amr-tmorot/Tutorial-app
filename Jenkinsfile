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
  }
}
