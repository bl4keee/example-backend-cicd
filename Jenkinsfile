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
          slackSend color: "good", message: "Message from Jenkins Pipeline"
        }
        failure {
          slackSend color: "red", message: "Message from Jenkins Pipeline"
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
