node {
    docker.image('maven').inside('-u root') {
        stage('Pull repository') {
            checkout scm
        }
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
        }
        stage('Stash jar file') {
            stash includes: 'target/server-0.0.1-SNAPSHOT.jar', name: 'binary'
        }
    }
}
node {
    stage('Unstash jar file') {
        unstash 'binary'
    }
    stage('Build and push Docker image') {
        def customImage = docker.build "bl4kee/basic-server"
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            customImage.push("$BUILD_NUMBER")
            customImage.push("latest")
        }
    }
}
