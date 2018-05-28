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
        stage('Docker image'){
          steps{
              sh "cd spring-boot-package-war && docker build -t gcr.io/my-gke-205110/my-java-app:${env.BUILD_NUMBER} ."
          }
        }
	stage('Push image to google container'){
          steps{
              sh "gcloud docker -- push gcr.io/my-gke-205110/my-java-app:${env.BUILD_NUMBER}"
          } 
        }
        stage('Deploy image'){
          steps{
             sh "kubectl run myjavaapp --image=gcr.io/my-gke-205110/my-java-app:${env.BUILD_NUMBER} --port=8080 && kubectl expose deployment myjavaapp --type=LoadBalancer --namespace jenkins"
          }
        } 
 
   }    
}
