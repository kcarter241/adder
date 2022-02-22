pipeline {
  agent {
    docker {
      label 'docker'
      image 'python:3'
    }
  }
  stages {
    stage('Compile') {
      steps {
        sh 'python3 -m compileall adder.py'
      }
    }
    stage('RUN') {
      steps {
        sh 'python3 adder.py 3 5'
      }
    }
    stage('Unit test') {
      steps {
        sh 'python3 -m unittest adder.py'
      }
    }
  }
}
