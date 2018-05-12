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

    stage("Test") {
      steps {
	      dir('spring-boot-package-war') {
            sh 'mvn test'
	      }
      }
    }
  }

  post {
    always {
      dir('spring-boot-package-war') {
        junit 'target/surefire-reports/**/*.xml'
      }
    }
  }
}
