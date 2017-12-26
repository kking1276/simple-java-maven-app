pipeline {
  agent {
    node {
      label 'mesos'
    }

  }
  stages {
    stage('first') {
      steps {
        sh '''mvn -B -DskipTests clean package'''
      }
    }
  }
}
