pipeline {
  
  agent any
  
  tools {
    maven 'Maven'
  }
  
  stages {
  
    stage("build") {
      steps {
        script {wrap([$class: 'BuildUser']) {sh 'echo "${BUILD_USER}"'}}
          echo 'building the application...'
          sh 'mvn -B -DskipTests clean package'
      }
      post {
        success {
           slackSend color: "good", message: 'Build started by ${specificCause} was successful!'
        }
        failure {
           slackSend color: "red", message: 'Build started by ${specificCause} failed!!'
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
