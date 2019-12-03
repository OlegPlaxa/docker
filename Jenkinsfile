pipeline {
    agent none
    stages {
        stage('Download') {
	parallel {
            stage('Centos_7') {
            agent {
                dockerfile { 
		    filename 'Dockerfile_yum_7'	
                    args '-u root -v /tmp:/download:rw'
                }
            }
            steps {
                sh """
                    yum install -y --downloadonly --downloaddir=/download nagios-plugins-all
                    ls -l /download
                """
            }}
	    stage('Centos_6') {
            agent {
                dockerfile {
                    filename 'Dockerfile_yum_6'
                    args '-u root -v /tmp:/download:rw'
                }
            }
            steps {
                sh """
                    yum install -y --downloadonly --downloaddir=/download nagios-plugins-all
                    ls -l /download
                """
            }}
        }}
	stage ('Checking') {
		agent {
			label 'master'
		}
		steps {
		sh """
			ls -l /tmp/nagios*	
		"""
		}
	}
    }
}