pipeline {
    agent any
    stages
    {
        stage('Git Clone')
        {
            steps{
            sh  'https://github.com/prashanth501/spring3hibernate'
            }
        stage('compile package')
        {
            steps{
            sh 'mvn package'
            }
        }
        
    }
            
