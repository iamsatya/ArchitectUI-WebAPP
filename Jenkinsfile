pipeline {
	agent any
	stages {
		stage('github') {
			steps {
				git credentialsId: 'git-creds', url: 'https://github.com/iamsatya/ArchitectUI-WebAPP.git'
			}
		}
		
		stage(maven) {
			steps {
				sh '/opt/maven/bin/mvn package'
			}
		}
		
		stage(tomcat) {
			steps {
				deploy adapters: [tomcat8(credentialsId: 'tomcat-creds',
				path: '',
				url: 'http://13.233.254.93:8080/')],
				contextPath: 'webapp',
				war: 'target/*.war'
				}
			}
		}
	}
