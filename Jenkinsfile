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
				sh 'mvn failsafe:integration-test failesafe:verify'
				
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
				script{
					dockerImage = docker.build("krisdocmac/currency-exchange:${$env.BUILD_TAG}")
				}
				
			}
		}
		stage('Push Docker Image'){
			steps {
			  script{
				  docker.withRegistry(' ','mydocker'){
				  dockerImage.push();
				  dockerImage.push("latest");
			         }
			  }
				
			}
		}

		
	}
}