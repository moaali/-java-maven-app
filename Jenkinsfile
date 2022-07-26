pipeline {
	agent any
	tools {
		maven 'Maven'
	}
	stages {
		stage 'Build JAR' {
			echo 'Building JAR...'
			echo 'Deploying...'
			sh 'maven package'
		}
		stage 'Build Image' {
			echo 'Building Image...'
			widthCredentials(usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')) {
				sh 'docker build -t moaali/java-maven-app:1.0'
				sh "echo $PASS | docker login -u $USER --password-stdin"
				sh 'docker push moaali/java-maven-app:1.0'
			}
		}
		stage 'Deploy' {
			echo 'Deploying...'
		}
	}
}