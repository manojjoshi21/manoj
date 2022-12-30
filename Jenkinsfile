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
                 timeout(1) {
                   def qg = waitForQualityGate()
                   if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                }
            }
           
        }
    }

 }
}
}
