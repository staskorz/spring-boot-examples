pipeline {
  agent any

  stages {
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

    success {
      dir('spring-boot-package-war') {
        script {
          currentBuild.description = readMavenPom().getFinalName()
        }
      }
    }
  }
}
