pipeline {
  agent any

  environment {
    MAVEN_HOME = '/usr/share/maven' // Adjust if needed
  }

  triggers {
    githubPullRequest() // PR-based trigger
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Building Java project...'
        sh 'mvn clean compile'
      }
    }

    stage('Unit Test') {
      steps {
        echo 'Running unit tests...'
        sh 'mvn test'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying application...'
        // Add your actual deploy script here
        sh './deploy.sh'
      }
    }
  }

  post {
    success {
      echo 'Build succeeded!'
    }
    failure {
      echo 'Build failed!'
    }
  }
}

