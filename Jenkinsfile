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
				    sshagent(['test']) {
                       sh """
                           scp -o StrictHostKeyChecking=no target/*.war test@192.168.33.10:/opt/apache-tomcat-8.5.46/webapps
						 
						   ssh test@192.168.33.10 /opt/apache-tomcat-8.5.46/bin/shutdown.sh
						 
						   ssh test8@192.168.33.10 /opt/apache-tomcat-8.5.46/bin/startup.sh
						   
                          """				  
                }
            }
        }
    }
}	
     
	 
