pipeline {
  agent none

  stages {
    stage('build') {
      agent {
          docker {
            image 'lilinj2000/dev:centos6'
          }
      }

      environment {
        home_3rd = '/var/jenkins_home/dist_pkg/3rd/centos6'
    	home_libs = '/var/jenkins_home/dist_pkg/libs/centos6'
    	home_app = '/var/jenkins_home/dist_pkg/app/centos6'
      }

      steps {
        sh '''
	./configure
	make
	'''
      }
    }

    stage('SonarQube analysis') {
      agent none

      steps {
        script {
          // requires SonarQube Scanner 2.8+
          scannerHome = tool 'SonarQube Scanner'
        }
        withSonarQubeEnv('SonarQube') {
          // tool name: 'scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	  sh 'env'
	  sh "${scannerHome}/bin/sonar-scanner"
        }
      }
    }
  }
}