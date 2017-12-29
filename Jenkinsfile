pipeline {
  agent {
    docker {
      image 'lilinj2000/dev:centos6'
    }
  }

  environment {
    home_3rd = '${env.HUDSON_HOME}/dist_pkg/3rd/centos6'
  }
  stages {
    stage('build') {
      steps {
        sh '''
	env
	./configure
	make
	'''
        cleanWs(cleanWhenSuccess: true)
      }
    }
  }
}