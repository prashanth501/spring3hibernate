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
				 sh 'mv target/*.war target/myweb.war'
		     }
		}
		    stage('code quality'){
			     steps{
				 sh 'mvn checkstyle:checkstyle; mvn findbugs:findbugs'
			 }
        }
            stage ('Code Coverage'){
                 steps{
                 sh ' mvn cobertura:cobertura'
            }
        }
		    stage("Building SONAR ...") {
                 steps{
                 sh './gradlew clean sonarqube'
                 }
                 } catch (e) {emailext attachLog: true, body: 'See attached log', subject: 'BUSINESS Build Failure', to: 'prashanth.kochu@gmail.com'
                 step([$class: 'WsCleanup'])
            stage ('Publish Cobertura'){
                 steps {
                 cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
            }
        }   
		    stage ('jacoco code coverage'){
			     steps {
			     jacoco exclusionPattern: '**/*Test*.class', inclusionPattern: '**/*.class', sourceExclusionPattern: 'generated/**/*.java'
			}
		}
            stage ('Publish findbugs'){
                 steps{
                 findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: ' **/findbugsXml.xml', unHealthy: ''

            
            }

        }
		    stage (deploying war file to target machine){
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

	
