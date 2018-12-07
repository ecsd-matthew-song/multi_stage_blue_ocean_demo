pipeline {
  agent any
  stages {
    stage('Build') {
      tools {
        maven 'maven'
      }
      environment {
        pom_directory = 'maven_test'
      }
      steps {
        echo 'Initiating maven build'
        sh 'mvn -f ${pom_directory}/pom.xml clean install'
        echo 'Maven build complete'
      }
    }
    stage('Testing') {
      parallel {
        stage('SonarQube Test') {
          steps {
            echo 'Initiating SonarQube test'
            echo 'SonarQube test Complete'
            withSonarQubeEnv('sonar') {
              sh 'mvn sonar:sonar -f ${pom_directory}/pom.xml'
            }

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
}