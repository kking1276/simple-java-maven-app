pipeline {
  agent any
  stages {
    stage('first') {
      steps {
        sh '''mvn -B -DskipTests clean package'''
      }
    }
  }
}
