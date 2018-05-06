pipeline{
    
    agent {
        any
    }

    stages{
        stage('Build'){
            steps{
                sh "cd spring-boot-package-war && mvn clean package"
            }
        }
        
    }
}