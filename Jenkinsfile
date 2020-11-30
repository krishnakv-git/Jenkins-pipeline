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
			//dockerHome = tool 'myDocker'
			mavenHome = tool 'MyMaven'
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