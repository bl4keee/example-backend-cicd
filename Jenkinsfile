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
         script {
             env.AUTHOR_NAME = sh(script: 'git show -s --pretty=%an', returnStdout: true)
         }
      }
      
      post {
        success {
           slackSend color: "good", message: 'Build successful on branch: ' + "${GIT_BRANCH}" + 
                                             '\nStarted by: ' + "${env.AUTHOR_NAME}" + 
                                             '\nTriggered by commit: ' + "${GIT_COMMIT.substring(0,6)}" +
                                             '\nCheck this build: ' + "${BUILD_URL}"
        }
        failure {
           slackSend color: "red", message: 'Build failure on branch: ' + "${GIT_BRANCH}" + 
                                            '\nStarted by: ' + "${env.AUTHOR_NAME}" + 
                                            '\nTriggered by commit: ' + "${GIT_COMMIT.substring(0,6)}" + 
                                            '\nCheck this build: ' + "${BUILD_URL}"
        }
      }
    }
    
    stage("test") {
      steps {
        echo 'testing the application...'
        sh 'mvn test'
      }
    }
    
    stage('Sonarqube analysis') {
        
        environment {
            scannerHome = tool 'sonar'
        }
        
        steps {
            withSonarQubeEnv('sonarqube') {
                sh 'mvn clean package sonar:sonar'
            }
        }
    }
    
    stage("deploy") {
      steps {
        echo 'deploying the application...'
        sh 'mvn clean deploy:heroku'
      }
    } 
  }
}
