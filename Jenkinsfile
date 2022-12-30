pipeline{
    agent any
    stages{
        stage("Sonar Quality Check"){
            
            steps{
                script{
                   withSonarQubeEnv(credentialsId: 'sonarmanoj') {
                     sh 'chmod +x gradlew'
                     sh './gradlew sonarqube' 
    
                 }
                }
            }
           
        }
    }

}
