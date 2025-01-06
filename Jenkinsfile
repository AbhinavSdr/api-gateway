pipeline {	
	agent any	
	tools {	    
		maven 'my-maven'		
		jdk 'jdk-17'	
	}	
	stages {        
		stage('Clone'){			
			steps {git url:'https://github.com/AbhinavSdr/api-gateway.git', branch:'master'}
		}
		stage('Build'){			
			steps {bat "mvn clean install -DskipTests"}		
		}	
        stage('Pre-Deploy'){
			steps{bat "docker rm -f api-gateway-cntr"
						"docker rmi -f gateway-img"}
		}	
		stage('Deploy') {			
			steps { bat "docker build -t gateway-img ."			    
			            bat "docker run -p 9060:8060 -d --name api-gateway-cntr --network my-net gateway-img"}		
		}		
	}
}