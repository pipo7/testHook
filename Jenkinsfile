pipeline {
    
     agent any
    
    stages {
        stage ('Compilation first Stage') {

            steps {
                
                    sh 'mvn clean compile'
                
            }
        }

        stage ('Testing Stage') {

            steps {
                
                    sh 'mvn test'
                
            }
        }


        stage ('Deployment Stage') {
            steps {
                 
                    sh 'mvn deploy'
                
            }
        }
    }
}