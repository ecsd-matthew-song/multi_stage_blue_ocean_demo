pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Initiating maven build'
        sh 'mvn -f ${POM_DIRECTORY}/pom.xml clean install'
        echo 'Maven build complete'
      }
    }
    stage('Testing') {
      parallel {
        stage('SonarQube Test') {
          environment {
            SONAR_HOST_URL = 'http://54.72.188.83:9000'
          }
          steps {
            echo 'Initiating SonarQube test'
            sh 'mvn sonar:sonar -f ${POM_DIRECTORY}/pom.xml -Dsonar.host.url=${SONAR_HOST_URL}'
            echo 'SonarQube test Complete'
          }
        }
        stage('Selenium Test') {
          steps {
            echo 'Initiating Selenium test'
            echo 'Selenium test complete'
          }
        }
      }
    }
    stage('Deploy prompt') {
      steps {
        input 'Deploy to Production?'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Initiating Deployment'
        echo 'Deployment Complete'
      }
    }
  }
  tools {
    maven 'maven'
  }
  environment {
    POM_DIRECTORY = 'jpetstore-6'
  }
}
