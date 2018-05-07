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
        
    }
}
