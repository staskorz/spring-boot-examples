pipeline {
  agent any

  stages {
    stage("Version") {
      steps {
        sh 'echo "Build version: ${BUILD_NUMBER}"'
      }
    }

    stage("Compile") {
      dir('spring-boot-package-war') {
        steps {
          sh 'mvn compile'
        }
      }
    }
  }
}
