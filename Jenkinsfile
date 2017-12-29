pipeline {
  agent {
    docker { image 'lilinj2000/dev:centos6' }
  }
  stages {
    stage('build') {
      steps {
        sh '''
	env
	uname -a
	sleep 10000
	'''
      }
    }
  }
}