pipeline {
  
  agent any
    
  tools {
    maven 'Maven'
  }
  
  stages {
  
    stage("build") {
      steps {
         echo 'building the application...'
         sh 'mvn -B -DskipTests clean package'
      }
      
      post {
        success {
           slackSend color: "good", message: 'Build successful on branch - ' + "${GIT_BRANCH}" + '\nStarted by:' + "${CHANGE_AUTHOR}" + '\nTriggered by commit: ' + "${GIT_COMMIT.substring(0,6)}" + '\nCheck this build: ' + "${BUILD_URL}'
        }
        failure {
           slackSend color: "red", message: 'Build failure on branch - ' + "${GIT_BRANCH}" + '\nStarted by:' + "${CHANGE_AUTHOR}" + '\nTriggered by commit: ' + "${GIT_COMMIT.substring(0,6)}" + '\nCheck this build: ' + "${BUILD_URL}'
        }
      }
    }
    
    stage("test") {
      steps {
        echo 'testing the application...'
        sh 'mvn test'
      }
    }
    
    stage("deploy") {
      steps {
        echo 'deploying the application...'
      }
    } 
  }
}
