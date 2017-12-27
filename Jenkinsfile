pipeline {
  agent {
    node {
      label 'mesos'
    }

  }
  // Apache Maven related side notes:
    // --batch-mode : recommended in CI to inform maven to not run in interactive mode (less logs)
    // -V : strongly recommended in CI, will display the JDK and Maven versions in use.
    //      Very useful to be quickly sure the selected versions were the ones you think.
    // -U : force maven to update snapshots each time (default : once an hour, makes no sense in CI).
    // -Dsurefire.useFile=false : useful in CI. Displays test errors in the logs directly (instead of
    //                            having to crawl the workspace files to see the cause).
    //sh "mvn --batch-mode -V -U -e clean deploy -Dsurefire.useFile=false"
  stages {
    stage('Clean') {
      steps {
        sh 'mvn -B -DskipTests clean'
      }
    }
    stage('Compile') {
      steps {
        sh '''mvn -B -DskipTests compile'''
      }
    }
    stage('Test') {
      steps {
        sh '''mvn -B -DskipTests test'''
      }
    }

    stage('Package') {
      steps {
        sh '''mvn -B -DskipTests package'''
      }
    }
  }
}