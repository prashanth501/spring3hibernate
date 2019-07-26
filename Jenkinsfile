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
            stage ('Publish Cobertura'){
                 steps {
                 cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
            }
        }
            stage ('Publish findbugs'){
                 steps{
                 findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: ' **/findbugsXml.xml', unHealthy: ''

            
                }

            }
        }			 
	}			 

		

	
