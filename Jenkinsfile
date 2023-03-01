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
				sh 'git clone https://github.com/rakesh-2502/Amazon.git '
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
			post {
				always {
				    dir ('Amazon'){
					    junit 'Amazon/Amazon-Core/target/surefire-reports/*.*xml'
					    archiveArtifacts artifacts: 'Amazon/Amazon-Core/target/*.jar', followSymlinks: false
					    archiveArtifacts artifacts: 'Amazon/Amazon-Web/target/*.war', followSymlinks: false
				    }
				}
			}
		}
		
		stage ('run') {
			    steps {
			        dir ('Amazon/Amazon/Amazon-Web') {
			        sh 'cp target/*.war /opt/tomcat/webapps'
			        }
			    }
			}   
		stage ('tomcat') {
			    steps {
			        dir ('/opt/tomcat/bin') {
			        sh 'sh startup.sh ;sleep 10s'
			        }
			    }
			}  
		
			}
}
