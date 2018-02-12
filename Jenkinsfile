pipeline {
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


  stages {
    stage('code static check') {
      steps {
        sh '''
cpplint --output=vs7 --recursive .
cppcheck --enable=all --inconclusive --xml --xml-version=2 . 2> cppcheck.xml
cppcheck-htmlreport --title="$JOB_NAME" --file=cppcheck.xml  --report-dir=./cppcheck-report
	'''
	archiveArtifacts 'cppcheck.xml'
	archiveArtifacts 'cppcheck-report/*'

	publishHTML([allowMissing: false,
	 alwaysLinkToLastBuild: false,
	 keepAll: false,
	 reportDir: 'cppcheck-report',
	 reportFiles: 'index.html',
	 reportName: 'cppcheck report',
	 reportTitles: ''])

      }
    }

    stage('build') {

      steps {
        sh '''
	./configure
	make
	'''
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

  post { 
    always { 
      cleanWs()
     }
  }

}