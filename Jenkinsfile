pipeline {
  agent { dockerfile { label 'docker' } }
  parameters {
    string defaultValue: 'main', description: 'Commit to biuld', name: 'REF', trim: true
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
        sh '''python3 -m pytest \
              -v --junitxml=junit.xml \
              --cov-report xml --cov adder adder.py
        '''
      }
    }
    stage('Hello GitHub') {
      steps {
	echo 'Hello GitHub!'
      }
    }
  }
  post {
    always {
      junit 'junit.xml'
      cobertura coberturaReportFile: 'coverage.xml'
    }
  }
}
