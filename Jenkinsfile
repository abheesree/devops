pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build WAR file') {
      when {
        // Don't build the WAR file if it already exists
        expression { sh('ls target/my-app.war').trim().isEmpty() }
      }

      steps {
        // Build the WAR file
        sh 'mvn clean package'
      }
    }

    stage('Deploy WAR file to Nexus') {
      steps {
        // Upload the WAR file to Nexus
        nexusArtifactUploader artifacts: 'target/my-app.war',
          nexusUrl: 'http://localhost:8081/nexus',
          repository: 'my-repository'
      }
    }
  }