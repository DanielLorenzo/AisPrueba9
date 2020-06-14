pipeline {
    tools {
      maven "Maven 3.9.9"
      jdk 'jdk8'
    }
    agent any
    stages {
      stage("Preparation") {
        steps {
          checkout scm
        }
      }
      stage("Compile") {
        steps {
          sh 'mvn clean compile'
        }
      }
      stage("Test") {
        steps {
          sh 'mvn test'
        }
      }
      stage("Install") {
        steps {
          sh 'mvn install -Dmaven.test.skip=true'
        }
      }
    }
    post {
       always {
 	    junit "**/target/surefire-reports/TEST-*.xml"
       }
       success {
         archiveArtifacts artifacts: '**/target/*.jar, **/target/*.war', fingerprint: true
       }
    }
}
