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
	cpplint --output=vs7 --recursive .
	cppcheck --enable=all --inconclusive --xml --xml-version=2 . 2> cppcheck.xml
	cppcheck-htmlreport --title="jetta" --file=cppcheck.xml  --report-dir=./cppcheck-report
	./configure
	make
	'''
	archiveArtifacts 'cppcheck.xml'
	archiveArtifacts 'cppcheck-report/*'

	publishHTML([allowMissing: false,
	 alwaysLinkToLastBuild: false,
	 keepAll: false,
	 reportDir: 'cppcheck-report',
	 reportFiles: 'index.html',
	 reportName: 'cppcheck Report',
	 reportTitles: ''])
      }
    }

/*
    stage('SonarQube analysis') {
      agent {
      	label 'master'
      }

      steps {
        script {
          scannerHome = tool 'SonarQube Scanner'
        }
        withSonarQubeEnv('SonarQube') {
	  sh 'env'
	  sh "${scannerHome}/bin/sonar-scanner"
        }
      }
    }
*/
  }
}