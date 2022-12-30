pipeline{
    agent any
    environment{
        VERSION="${env.BUILD_ID}"
    }
    stages{
        stage("Sonar Quality Check"){
            
            steps{
                script{
                   withSonarQubeEnv(credentialsId: 'sonarmanoj') {
                     sh 'chmod +x gradlew'
                     sh './gradlew sonarqube' 
    
                 }
                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                
                }
            }
           
        }
    }

 }
 stage("docker build and docker push"){
    steps{
        script{
         withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_pass')]) {
         sh '''
            docker build -t 52.66.244.15:8085/springapp:${VERSION} .
            docker login -u admin -p $docker_pass 52.66.244.15:8085
            docker push 52.66.244.15:8085/springapp:${VERSION}
            docker rmi 52.66.244.15:8085/springapp:${VERSION}
            '''
        }
    }
 }
  
    }
}
}
        
