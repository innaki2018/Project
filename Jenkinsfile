pipeline{
    
    agent {
      label 'jenkins-slave'
    }

    stages{
        stage('Build.${env.BUILD_NUMBER}'){
            steps{
                sh "cd spring-boot-package-war && mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} &&  mvn clean package "
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
