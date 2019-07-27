pipeline {
    agent any
    stages{
        stage('Git Clone'){
            steps{
            git credentialsId: '975bcc7c-cd09-431f-bdfa-00a8fd1039b0', url: 'https://github.com/prashanth501/spring3hibernate.git'
            }
		}
        stage('compile package'){
            steps{
            sh 'mvn package'
            }
        }
    }
}
