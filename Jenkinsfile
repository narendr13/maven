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
				sh "mvn -Dmaven.test.failure.ignore=true install"
				sh "mv target/*.war target/project.war"
				
			}
		}
		stage("deploy"){
			steps{
			sshagent(['tomcat']) {
    				sh """
					scp -o StrictHostKeyChecking=no target/*.war ubuntu@10.1.1.154:/opt/tomcat/webapps/
					
					ssh ubuntu@10.1.1.154 /opt/tomcat/bin/shutdown.sh
					
					ssh ubuntu@10.1.1.154 /opt/tomcat/bin/startup.sh
				"""
			}
		}
		}
	}
}
