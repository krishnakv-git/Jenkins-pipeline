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
		stage('checkout'){
			steps{
				sh 'mvn --version'
				echo "PATH - $PATH"
			}
		}
		stage('Compile'){
			steps {
				sh 'mvn clean compile'

			}
		}
		stage('Test'){
			steps {
				sh 'mvn test'
				
			}
		}
		stage('Integration test'){
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
				
			}
		}
	}
}
