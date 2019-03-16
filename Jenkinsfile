pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn clean compile'
                }
            }
        }
        
        agent any
        
        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn test'
                }
            }
        }
        
        agent slave2
        
        stage ('Build on Slave Stage') {

            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn package'
                }
            }
        }
        
        agent any

        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'Apache Maven 3.5.2') {
                    sh 'mvn install'
                }
            }
        }
    }
}
