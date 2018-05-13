pipeline{
    
    agent any

    stages{
        stage('Build'){
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
     post {
         success{
               sh "cp ${env.JENKINS_HOME}/jobs/${env.JOB_NAME}/builds/${env.BUILD_NUMBER}/archive/spring-boot-package-war/target/spring-boot-package-war-${env.BUILD_NUMBER}.war /var/lib/tomcat7/webapps/myapp"
         }
     }
    
}
