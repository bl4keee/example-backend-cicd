pipeline {
  
  agent any
  
  stages {
  
    stage("build") {
      steps {
        echo 'building the application...'
        maven('Maven') {
          sh 'mvn -B -DskipTests clean package'
        }
      } 
    }
    
    stage("test") {
      steps {
        echo 'testing the application...'
        maven('Maven') {
          sh 'mvn test'
        }
      }
    }
    
    stage("deploy") {
      steps {
        echo 'deploying the application...'
      }
    }
  }
}
