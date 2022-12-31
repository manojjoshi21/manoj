pipeline{
    agent any
    stages{
      stage('indentifying misconfigs using datree in helm charts'){
        steps{
            script{
                dir('kubernetes/'){
	         withEnv(['DATREE_TOKEN=0039d72c-a82a-4b0c-ad3c-fd920b0d0afb']) {
                 sh 'helm datree test myapp/'
                }
		}
            }
        }
    }
        


 }
}






    

        
