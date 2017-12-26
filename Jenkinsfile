pipeline {
  agent {
    node {
      label 'mesos'
    }
    
  }
  stages {
    stage('first') {
      steps {
        sh '~/apache-maven-3.5.2/bin/mvn -B -DskipTests clean package'
      }
    }
  }
}