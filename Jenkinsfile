pipeline {
  agent {
    docker {
      image 'bitwiseman/training-blueocean-sample'
      args '-u root -v $HOME/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        parallel(
          "Build": {
            sh './jenkins/build.sh'
            
          },
          "Archive the Artifacts": {
            sh 'target/*.war'
            
          }
        )
      }
    }
    stage('Test') {
      steps {
        sh './jenkins/test-all.sh'
      }
    }
    stage('Publish JUnit') {
      steps {
        sh '**/surefire-reports/**/*.xml'
      }
    }
    stage('Publish JUnit test result report') {
      steps {
        sh '**/test-results/karma/*.xml'
      }
    }
  }
}