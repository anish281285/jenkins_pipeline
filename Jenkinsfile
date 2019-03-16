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
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn clean sonarqube'
                }
            }
        }
        
        
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn install'
                }
            }
        }
    }
}

