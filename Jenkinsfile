pipeline {
	environment {
		registry = "anildocker33/github-jenkins-docker"
		registryCredential = 'dockerhub'
		dockerImage = ''
		dockerRunCommand = 'docker run -d -p 8080:8080 -name myapp anildocker33/github-jenkins-docker'
	}
	agent any
	stages {
		stage("Building docker image") { 
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage("Pushing image to DockerHub") { 
			steps {
				script {
					docker.withRegistry( '', registryCredential ) {
						dockerImage.push()
						dockerImage.push( 'latest' )
					}
				}
			}
		}
	}
}
