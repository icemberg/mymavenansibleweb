pipeline {
	agent any
	tools {
		maven 'Maven'
	}
	stages {
		stage('Checkout') {
			steps {
				git branch: 'main', url: 'https://github.com/icemberg/mymavenansibleweb.git'
			}
		}
		stage('Build') {
			steps {
				sh 'mvn clean package'
			}
		}
		stage('Archive') {
			steps {
				archiveArtifacts artifacts: 'target/mymavenansibleweb.war', fingerprint:true
			}
		}
		stage('Deploy') {
			steps {
				sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
			}
		}
	}
	post {
		success {
			print 'Deployment successful'
		}
		failure {
			print 'Deployment failed'
		}
	}
}
