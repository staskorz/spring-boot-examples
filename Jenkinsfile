pipeline {
  agent any

  stages {
    stage("Version") {
      steps {
        sh "echo 'Build version: ${BUILD_NUMBER}'"
      }
    }

    stage("Compile") {
      steps {
	    dir('spring-boot-package-war') {
          sh 'mvn compile'
	    }
      }
    }
  }
}
