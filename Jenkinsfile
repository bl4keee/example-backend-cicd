pipeline {
  
  agent any
  
  tools {
    maven 'Maven'
  }
  
  stages {
  
    stage("build") {
      steps {
        wrap([$class: 'BuildUser']) {
          def user = env.BUILD_USER_ID
          echo 'building the application...'
          sh 'mvn -B -DskipTests clean package'
        }
      }
      post {
        success {
           slackSend color: "good", message: 'Build started by ${user} was successful!'
        }
        failure {
           slackSend color: "red", message: 'Build started by ${user} failed!!'
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
