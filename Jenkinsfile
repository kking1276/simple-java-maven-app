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
        sh 'git status'
//        input message: 'Continue?', ok: 'Continue'
        sh 'mvn -B -DskipTests clean'
      }
    }
    stage('Compile') {
      steps {
        sh '''mvn -B -DskipTests compile'''
        stash name: 'sources', includes: 'pom.xml,src/,target/'
      }
    }

    stage('Test') {
      steps {
       	script {
			def splits = splitTests count(3)
			def branches = [:]
			for (int i = 0; i < splits.size(); i++) {
			  def index = i // fresh variable per iteration; i will be mutated
			  branches["split${i}"] = {
			    node('mesos') {
			      deleteDir()
			      unstash 'sources'
			      def exclusions = splits.get(index);
			      writeFile file: 'exclusions.txt', text: exclusions.join("\n")
//			      sh "${tool 'M3'}/bin/mvn -B -Dmaven.test.failure.ignore -Dsurefire.excludesFile=exclusions.txt test"
			      sh "mvn -B -Dmaven.test.failure.ignore -Dsurefire.excludesFile=exclusions.txt test"
			      junit 'target/surefire-reports/*.xml'
			    }
			  }
			}
			parallel branches
       	}
      }
    }

    stage('Package') {
      steps {
        sh '''mvn -B -DskipTests package'''
      }
    }
  }
}