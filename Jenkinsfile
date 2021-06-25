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
		
		stage(nexus) {
			steps {
				nexusPublisher nexusInstanceId: 'nexus-repo',
				nexusRepositoryId: '',
				packages: [[$class: 'MavenPackage',
				mavenAssetList: [[classifier: '',
				extension: '', filePath: '{WORKSPACE}/target/*.war']],
				mavenCoordinate: [artifactId: 'watr',
				groupId: 'com.govanin', packaging: 'war',
				version: '1.0']]], tagName: '1.0'
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
