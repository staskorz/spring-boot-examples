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

    stage("Deploy") {
      steps {
	      dir('spring-boot-package-war') {
          script {
            name = readMavenPom().getName()
            version = readMavenPom().getVersion()
            sh "scp target/${name}-${version}-${BUILD_NUMBER}.war ubuntu2:/var/lib/tomcat7/webapps/ROOT.war"
          }
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
          name = readMavenPom().getName()
          version = readMavenPom().getVersion()
          currentBuild.description = "${name}-${version}-${BUILD_NUMBER}"
        }

        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
      }
    }
  }
}
