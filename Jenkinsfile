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
    stage('Deploy'){
        steps{
            sh "docker run -v /${env.JENKINS_HOME}/jobs/${env.JOB_NAME}/lastSuccessful/archive/spring-boot-package-war/target/spring-boot-package-war-${env.BUILD_NUMBER}.war:/usr/local/tomcat/webapps/myapp -p 7070:8080 -d tomcat"
        }
    }
        
    }
}
