#!groovy

pipeline {
  agent none

  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.8.6-openjdk-8'
          args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
      }
      steps {
        sh 'mvn clean install -Dcheckstyle.skip=true'
      }
    }

    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t grupo02/spring-petclinic:latest .'
      }
    }
  }
}
