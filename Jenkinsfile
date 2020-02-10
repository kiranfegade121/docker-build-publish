pipeline {
	
	agent any 
		
	stages {
	
	    stage("checkout from SCM") {
		    steps {
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kiranfegade121/hello-world-rest-api.git']]])
		    } 	    
		}
	
		stage("build and archieve an artifact") {
			steps {
				echo "Building an artifact..."
				sh label: '', script: 'mvn clean package'
				echo "Archiving an artifact..."
				archiveArtifacts '**/*.jar'
			}
		}
		
		stage("build an image") {
			steps {
				echo "creating an image..."
				withCredentials([usernamePassword(credentialsId: 'docker-hub-cred', passwordVariable: 'PASSWORD', 			usernameVariable: 'USERNAME')]) {
					sh label: '', script: 'docker login -u $USERNAME -p $PASSWORD'
					sh label: '', script: 'docker build -t kiranfegade/hello-world-rest-api:3.0 .'
				}
			}			
		}
		
		stage("push docker image") {
			steps {
				sh label: '', script: 'docker push kiranfegade121/hello-world-rest-api:3.0'
			}
		}
		
		
	}
}			
