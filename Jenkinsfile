pipeline{
    
    agent {
      label 'jenkins-slave'
    }

    stages{
        stage('Build'){
            steps{
                sh "cd spring-boot-package-war && mvn clean package -Drevision=${BUILD_NUMBER} "
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
