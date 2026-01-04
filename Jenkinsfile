
// Jenkinsfile (Declarative Pipeline)
pipeline {
  agent any

  options {
    timestamps()
    disableConcurrentBuilds()
  }

  stages {
    stage('Checkout') {
      steps {
        // If your job is "Pipeline script from SCM", Jenkins auto-checkouts.
        // This makes it explicit and also works for inline pipelines.
        checkout scm
      }
    }

    stage('Compile') {
      steps {
        sh '''
          set -euxo pipefail
          chmod +x mvnw
          ./mvnw -B -ntp clean compile
        '''
      }
    }

    stage('Test') {
      steps {
        sh './mvnw -B -ntp test'
      }
    }

    stage('Publish Reports') {
      steps {
        junit 'target/surefire-reports/*.xml'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true, onlyIfSuccessful: true
      }
    }
  }
}
