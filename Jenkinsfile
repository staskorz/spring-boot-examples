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
      script {
        currentBuild.description = "${env.JOB_NAME}-${version}"
      }
    }
  }
}
//script {
//            sh "mvn -B versions:set -DnewVersion=1.0-SNAPSHOT-${env.BUILD_NUMBER} && mvn clean package"
//            version = readMavenPom().getVersion()
//            currentBuild.description = "${env.JOB_NAME}-${version}"
//          }
