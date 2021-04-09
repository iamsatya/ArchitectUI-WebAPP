pipeline {
	agent any
	stages {
		stage('pull') {
			steps {
				checkout(
				[$class: 'GitSCM',
				branches: [[name: '*/master']],
				extensions: [],
				userRemoteConfigs: [[credentialsId: 'github-creds', url: 'https://github.com/iamsatya/ArchitectUI-WebAPP.git']]])
			}
		}
				
		stage(build) {
			steps {
				sh 'mvn package'
			}
		}
		stage(deploy) {
			steps {
				deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://35.154.159.251:8080')], contextPath: 'pipe', war: 'target/*.war'
				}
			}
		}
	}
