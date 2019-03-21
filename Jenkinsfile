pipeline {
    agent { label 'mavenlabel' }

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn clean compile'
                }
            }
        }
        
            
        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn test'
                }
            }
        }
        
                
        stage ('Build on Slave Stage') {

            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn package'
                }
            }
        }
        
        
        stage ('Building and Integrating Sonar') {

            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn package sonar:sonar'
                }
            }
        }
        
        
         stage ('Deployment Stage') {
            
             steps {
                sshagent(['tomcat-dev']) {
                    sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@13.234.116.209:/var/lib/tomcat/webapps'
                }
            }
        }
    }
}

