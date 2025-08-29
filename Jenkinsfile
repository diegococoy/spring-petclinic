#!groovy

pipeline {
  agent any

  tools {
    maven 'Maven3'
  }

  environment {
    SONAR_SCANNER_HOME = tool 'SonarQubeScanner'
    SONAR_PROJECT_KEY = 'sonar-petclinic'
  }

  stages {
    stage('Maven Install') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
      steps {
        sh 'docker build -t grupo02/spring-petclinic:latest .'
      }
    }
    stage('SonoarQube Analysis') {
      steps {
        withCredentials([string(credentialsId: 'sonar-petclinic-token', variable: 'SONAR_TOKEN')]) {
          withSonarQubeEnv('SonarQube02') {
            sh """
            ${SONAR_SCANNER_HOME}/bin/sonar-scanner \ 
            -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
            -Dsonar.host.url=https://localhost:9000 \
            -Dproject.login$={SONAR_TOKEN}
            """
          }
        }
      }
    }
  }
}
