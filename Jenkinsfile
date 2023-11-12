pipeline {
  agent any
<<<<<<< HEAD
  
  environment {
        MAVEN_HOME = tool 'mvn' // Assumes "Maven" is configured in Jenkins tools
    }
  
=======

  environment {
        MAVEN_HOME = tool 'mvn' // Assumes "Maven" is configured in Jenkins tools
    }

>>>>>>> 1b7d530 (test)
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build WAR file') {
      // when {
      //   // Don't build the WAR file if it already exists
      //   expression { sh(script: 'ls target/myweb-8.2.0.war', returnStatus: true) == 0 && sh(script: 'ls target/myweb-8.2.0.war', returnStdout: true).trim().isEmpty() }
<<<<<<< HEAD
      // }
      when {
        // Don't build the WAR file if it already exists
        expression { sh(script: 'ls target/myweb-8.2.0.war', returnStatus: true) == 0 && sh(script: 'ls target/myweb-8.2.0.war', returnStdout: true).trim().isEmpty() }
=======
>>>>>>> 1b7d530 (test)

      // }

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
}
