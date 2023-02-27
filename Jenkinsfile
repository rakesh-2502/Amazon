pipeline {
	agent any
	stages {
	    stage ('clean up') {
	        steps {
	            cleanWs()
	        }
	    }
	    stage ('clone') {
			steps {
				sh 'git clone https://github.com/rakesh-2502/Amazon'
			}
		
		}
		stage ('build') {
			steps {
			    dir ('Amazon/Amazon'){
				    sh 'mvn clean install -DskipTests'
			    }
			}
		}
		stage ('test') {
			steps {
			    dir ('Amazon/Amazon'){
				    sh 'mvn test'
			    }
			}
			
		}
			}
	
}
