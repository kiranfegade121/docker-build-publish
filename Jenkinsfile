pipeline {
	
	agent any 
	
	tools {
		maven "MAVEN"
	}
	
	stages {
	
		stage("build and archieve an artifact") {
			steps {
				echo "Building an artifact..."
				bat label: '', script: 'mvn clean package'
				echo "Archiving an artifact..."
				archiveArtifacts '**/*.jar'
			}
		}
		
		stage("build an image") {
			steps {
				echo "creating an image..."
				script {
					app = docker.build("amitfegade121/hello-world-rest-api:3.0");
				}
			}			
		}
		
		stage("push docker image") {
			steps {
				script {
					withDockerRegistry(credentialsId: 'docker-hub-cred', url: 'https://registry.hub.docker.com') {
						app.push()
					}
				}
			}
		}
		
		
	}
}			