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
				echo "BUILD_URL - $env.BUILD_URL"
				echo "BUILD_TAG - $env.BUILD_TAG"
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
		stage('Package'){
			steps {
				sh 'mvn package -DskipTests'
				
			}
		}
		stage('Build Docker Image'){
			steps {
				//sh 'mvn test'
				script {
					dockerImage = docker.build("krisdocmac/currency-exchange:test")
				}
				
			}
		}
		stage('Push Docker Image'){
			steps {
			  script{
				  docker.withRegistry(' ','mydcoker'){
				  dockerImage.push();
				  dockerImage.push("latest");
			         }
			  }
				
			}
		}

		
	}
}
