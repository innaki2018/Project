pipeline{
    
    agent any

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
              sh "docker run -p 7474:8080 -v ${env.JENKINS_HOME}/jobs/${env.JOB_NAME}/builds/${env.BUILD_NUMBER}/archive/spring-boot-package-war/target/spring-boot-package-war-${env.BUILD_NUMBER}.war:/usr/local/tomcat/webapps/myapp.war -d tomcat"
          }
      } 
     }
    
}
