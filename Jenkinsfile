pipeline {
	agent any
	stages {
		stage('GIT-Stage') {
			steps {
				git credentialsId: 'github-creds', url: 'https://github.com/iamsatya/ArchitectUI-WebAPP.git'
			}
		}
		stage(build) {
			steps {
				sh '/opt/maven/bin/mvn package'
			}
		}
		stage(deploy) {
			steps {
				deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://13.126.252.30:8080')],
				contextPath: 'demo-pipeline', war: 'target/*.war'
				}
			}
		}
	}
