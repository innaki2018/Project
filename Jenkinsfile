pipeline{
    
    agent {
      label 'k8s'
    }	

    stages{
        stage('Build/Test'){
            steps{
                sh "cd spring-boot-package-war && mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
            }
	}
	stage('Show Tests result'){
  	    steps{ 		
	       junit '**/target/surefire-reports/*.xml'     
 	    }		
	}
	stage('Archive'){
            steps{
                archiveArtifacts artifacts: '**/target/*.war' 
            }	
        }
    
     
      stage('Deploy Docker'){
          steps{
              sh "pwd && ls **/target/*.war"
          }
      } 
     }
    
}
