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
				sh "mvn --version"
				sh "docker version"
            }
        }
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}

		stage('test') {
            steps {
                sh "mvn test"
            }
        }
		stage('Integration Test') {
            steps {
                sh "mvn failsafe:integration-test failsafe:verify"
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