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
        stage('Build') {
            steps {
				echo "PATH - $PATH"
                echo 'Build'
				sh "mvn --version"
				sh "docker version"
            }
        }
		stage('test') {
            steps {
                echo 'test'
            }
        }
		stage('Integration Test') {
            steps {
                echo 'Integration Test'
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