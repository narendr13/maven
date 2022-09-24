pipeline{
	agent any
	environment{
		PATH = "/opt/maven/bin:$PATH"
	}
	stages{
		stage("Git Checkout"){
			steps{
				git credentialsId: '9db8ffcb-3284-41bc-b748-bf1b6750ccff', url: 'https://github.com/narendr13/maven.git'
			}
		}
		stage("Maven Build"){
			steps{
				sh "mvn clean package"
				sh "mv target/*.war target/project.war"
			}
		}
		stage("deploy"){
			steps{
			sshagent(['tomcat']) {
    				sh """
					scp -o StrictHostKeyChecking=no target/project.war ubuntu@10.1.1.154:/opt/tomcat/webapps/
					
					shh ubuntu@10.1.1.154 /opt/tomcat/bin/shutdown.sh
					
					shh ubuntu@10.1.1.154 /opt/tomcat/bin/startup.sh
				"""
			}
		}
		}
	}
}
