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
        
        
        stage ('Deployment Stage') {
            
             steps {
                sshagent(credentials: ['tomcat-dev']) {
                    sh 'scp -o StrictHostKeyChecking=no /home/ec2-user/JenkinsDirectory/workspace/NewPipelineJob2/target/*.jar ec2-user@13.234.116.209:/opt/tomcat/webapps/'

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
    }
}

