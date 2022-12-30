pipeline{
    agent any
    stages{
        stage("Sonar Quality Check"){
            
            }
            steps{
                script{
                   withSonarQubeEnv(credentialsId: 'SonarJenkins') {
                     sh 'chmod +x gradlew'
                     sh './gradlew sonarqube' 
    
                 }
                }
            }
           
        }
    }


