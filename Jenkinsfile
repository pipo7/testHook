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


        stage ('Deployment & Packaging Stage') {
            steps {
                 
                    sh 'mvn deploy'
                    sh 'mvn checkstyle:checkstyle'                
            }
        }
        stage('checkStyle Stage'){
            steps {
                step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**/target/checkstyle-result.xml', healthy:'5', unHealthy:'10'])
            }   
        }
    }
}
