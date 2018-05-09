pipeline {
  agent any

  stages {
    stage("Version") {
      steps {
        sh 'echo "Build version: ${BUILD_NUMBER}"'
      }
    }

    stage("Compile") {
      steps {
        sh 'cd spring-boot-package-war && mvn compile'
      }
    }
  }
}
