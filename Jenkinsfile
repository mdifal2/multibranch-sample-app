pipeline {
  agent {label 'linux'}
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
        // Example of manually setting it if you've installed a custom JDK
        JAVA_HOME = '/opt/java/openjdk' 
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }
  stages {
    stage('Build') {
      steps {
        sh './gradlew clean check --no-daemon'
      }
    }
  }
  post {
    always {
        junit(
          allowEmptyResults: true, 
          testResults: '**/build/test-results/test/*.xml'
        )
    }
  }
}
