pipeline {
  agent any
  
  tools {
          maven 'mvn'
      }
      environment {
        // Extract the Git repository name from the full branch reference
        // GIT_REPO_NAME = sh(script: 'echo ${GIT_BRANCH} | cut -d / -f 2', returnStdout: true).trim()
                GIT_REPO_NAME = sh(script: 'basename $(git config --get remote.origin.url .git)', returnStdout: true).trim()

    }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build WAR file2') {
      // when {
      //   // Don't build the WAR file if it already exists
      //   expression { sh(script: 'ls target/myweb-8.2.0.war', returnStatus: true) == 0 && sh(script: 'ls target/myweb-8.2.0.war', returnStdout: true).trim().isEmpty() }
      //   }      // }
      when {
            expression {
                // Only build when the repository name is "myProject"
                return GIT_REPO_NAME == 'devops'
            }
            }

      steps {
        // Build the WAR file
        //echo ${GIT_BRANCH}
        echo "Git Repository Name: ${GIT_REPO_NAME}"
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
