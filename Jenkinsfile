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
          wrap([$class: 'BuildUser']) {
            slackSend color: "good", message: 'Build started by "${BUILD_USER}" was successful!'
          }
        }
        failure {
          wrap([$class: 'BuildUser']) {
            slackSend color: "red", message: 'Build started by "${BUILD_USER}" failed!!'
          }
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
