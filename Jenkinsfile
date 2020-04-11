pipeline {
    agent any
	//agent {
   //     docker { image 'maven:3.6.3' }
   // }
	environment{
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
    stages {
        stage('Checkout') {
            steps {
				echo "PATH - $PATH"
                echo 'Build'
				echo "BUILD_TAG - $env.BUILD_TAG"
				sh "mvn --version"
				sh "docker version"
            }
        }
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}

		stage('Test') {
            steps {
                sh "mvn test"
            }
        }
		stage('Integration Test') {
            steps {
                sh "mvn failsafe:integration-test failsafe:verify"
            }
        }
		stage('package') {
            steps {
                sh "mvn package -DskipTests"
            }
        }

		stage('Build Docker Image') {
			steps{
				//docker build -t alicharkhi18/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage =docker.build("alicharkhi18/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image') {
			steps{
				script{
					docker.withRegistry('','dockerthub') {
						dockerImage.push();
						dockerImage.push('latest');
				}
			}
		}
    }
	post {
		always{
			echo 'I run always!!!'
		}
		success{
			echo 'I run when it succeeds!!'
		}
		failure{
			echo 'I run when it fails!!'
		}
	}
}