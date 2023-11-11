pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build WAR file') {

     tools { 
        maven 'mvn' 
        //jdk 'JAVA_HOME' 
      }

      when {
        // Don't build the WAR file if it already exists
	      expression { sh(script: 'ls /var/lib/jenkins/workspace/pipe1/target/myweb-8.2.0.war', returnStatus: true) == 0  }

      }
      steps {
        // Build the WAR file
        sh 'mvn clean package'
      }
    }

    stage('Deploy WAR file to Nexus') {
      steps {
        // Upload the WAR file to Nexus
        nexusArtifactUploader artifacts: 'target/myweb-8.2.0.war',
          nexusUrl: 'http://localhost:8081/nexus',
          repository: 'my-repository'
      }
    }
  }
}

