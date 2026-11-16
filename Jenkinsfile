pipeline {
  agent any

  tools {
    jdk 'JDK11'
    maven 'Maven3'
  }

  stages {
    stage('Source') {
      steps {
        git branch: 'master', url: 'https://github.com/ditindia8892/estore-backend.git'
      }
    }
    stage('Compile') {
      steps {
        sh 'mvn -B clean compile'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn -B test'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B package -DskipTests'
      }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
    }
    success {
      archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    }
  }
}
