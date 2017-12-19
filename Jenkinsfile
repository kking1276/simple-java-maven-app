pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /home/me/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('first') {
      steps {
        sh '''mvn -B -DskipTests clean package
'''
      }
    }
  }
}