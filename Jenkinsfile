pipeline {
	agent {
		dockerfile {
			label 'docker'
			// image 'python:3'
		}
	}
	parameters {
		string(name: 'REF', defaultValue: '\${ghprbActualCommit}', description: 'Commit to build')
	}
	stages {
		stage('Hello Github') {
			steps {
				echo 'Hello Github!'
			}
		}
		stage('Compile') {
			steps {
				sh 'python3 -m compileall adder.py'
			}
		}
		stage('Run') {
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
	}
	post {
		always {
			junit 'junit.xml'
			cobertura coberturaReportFile: 'coverage.xml'
		}
	}
}