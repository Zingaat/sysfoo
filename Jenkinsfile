pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'compile maven app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'test maven app'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'package maven app'
        sh 'mvn package -DskipTests'
      }
    }

    stage('Docker Build and Publish.') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dashmo') {




            def dockerImage = docker.build("dashmo/sysfoo:v1{env.BUILD_ID}", "./")




            dockerImage.push()




            dockerImage.push("latest")




          }
        }

      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}