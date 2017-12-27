pipeline {
  agent {
    node {
      label 'mesos'
    }
    
  }
  stages {
    stage('first') {
      steps {
        sh 'mvn -B -DskipTests clean'
      }
    }
    stage('Compile') {
      steps {
        sh '''mvn -B -DskipTests compile
'''
      }
    }
  }
}