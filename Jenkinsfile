    pipeline {
        agent any
            stages {
                stage('git clone') {
                    steps{
                    git credentialsId: '975bcc7c-cd09-431f-bdfa-00a8fd1039b0', url: 'https://github.com/prashanth501/spring3hibernate.git'
                }
            }
		        stage('mvn '){
		            steps{
			        sh 'mvn package'
				  
		        }
		    }
		        
		        stage ('deploying war file to target machine'){
			        steps{
				    sshagent(['tomcat-new']) {
                       sh """
                           scp -o StrictHostKeyChecking=no target/myweb.war tomcat8@192.168.33.10:/opt/apache-tomcat-8.5.46/webapps
						 
						   ssh tomcat8@192.168.33.10 /opt/apache-tomcat-8.5.46/bin/shutdown.sh
						 
						   ssh tomcat8@192.168.33.10 /opt/apache-tomcat-8.5.46/bin/startup.sh
						   
                          """				  
                }
            }
        }
    }
}	
     
	 
