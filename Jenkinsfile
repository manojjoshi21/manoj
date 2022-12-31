pipeline{
    agent any
    environment{
        VERSION="${env.BUILD_ID}"
    }
    stages{
      stage('indentifying misconfigs using datree in helm charts'){
        steps{
            script{
                dir('kubernetes/'){
                 sh 'datree test myapp/*.yaml'
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



    

        
