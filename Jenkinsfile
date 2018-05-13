pipeline {
  agent any

  stages {
    stage("Version") {
      steps {
        sh "echo 'Build version: ${BUILD_NUMBER}' ${env.POM_DISPLAYNAME} ${env.POM_VERSION}"
      }
    }

    stage("Compile") {
      steps {
	      dir('spring-boot-package-war') {
            sh 'mvn clean compile'
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

    stage("Package") {
      steps {
	      dir('spring-boot-package-war') {
            sh 'mvn package'
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
