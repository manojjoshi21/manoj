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

    stage('indentifying misconfigs using datree in helm charts'){
        steps{
            script{
                dir('kubernetes/'){
                 sh 'helm datree test myapp/'
                }
                
            }
        }
    }
        


 }

post {
		always {
			mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "joshi.manoj2121@gmail.com";  
		 }
	   }
}



    

        
