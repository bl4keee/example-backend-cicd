pipeline {
  
  agent any
  
  stages {
  
    stage("build") {
      steps {
        echo 'building the application...'
        def mavenBuildContainer = docker.image('maven')
        mavenBuildContainer.pull()
        mavenBuildContainer.inside {
          sh 'mvn -B -DskipTests clean package'
        }
      } 
    }
    
    stage("test") {
      steps {
        echo 'testing the application...'
        def mavenTestContainer = docker.image('maven')
        mavenTestContainer.pull()
        mavenTestContainer.inside {
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
