/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
}
*/
//Declarative
pipeline {
	agent any 
		environment {
			dockerHome = tool 'myDocker'
			mavenHome = tool 'myMaven'
			path= "$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build'){
			steps{
				sh 'mvn --version'
			}
		}
	}
}