pipeline{
    
    agent {
      label 'jenkins-slave'
    }

    stages{
        stage('Build'){
            steps{
                sh "cd spring-boot-package-war && mvn clean package"
            }
	}
	stage('Test'){
  	    steps{ 		
	       junit '**/target/surefire-reports/*.xml'     
 	    }		
	}
	stage('Archive'){
            steps{
                archiveArtifacts artifacts: '**/target/*.war' 
            }	
        }
        
    }
}
