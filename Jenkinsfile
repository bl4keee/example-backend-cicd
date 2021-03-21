pipeline {
  
  agent { docker { image 'maven:3.3.3' } }
  
    stages {
      stage("build") {
        steps {
          echo 'building the application...'
          sh 'mvn -B -DskipTests clean package'
          }
      } 
    
      stage("test") {
        steps {
          echo 'testing the application...'
          sh 'mvn test'
          }
      }
    }
}
