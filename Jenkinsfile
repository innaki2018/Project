pipeline{
    
    agent any

    stages{
        stage('Build'){
            steps{
                sh "cd spring-boot-package-war && mvn clean package"
            }
	}
	stage('Test'){
  	    steps{ 		
	       sh "cd spring-boot-package-war && mvn test"     
 	    }		
	}
	stage('Archive'){
            steps{
                archiveArtifacts artifacts: '**/target/*.war' 
            }	
        }
        
    }
}
