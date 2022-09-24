pipeline{
	agent any
	environment{
		PATH = "/opt/maven/bin:$PATH"
	}
	stages{
		stage("Git Checkout"){
			steps{
				git credentialsId: '9db8ffcb-3284-41bc-b748-bf1b6750ccff', url: 'https://github.com/narendr13/VProfile.git'
			}
		}
		stage("Maven Build"){
			steps{
				sh "mvn clean package"
			}
		}
	}
}
