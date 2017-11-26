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
                    sh 'mvn pmd:pmd'   
                    sh 'mvn findbugs:findbugs'   
            }
        }
        stage('checkStyle publish Stage'){
            steps {
                step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**/target/checkstyle-result.xml', healthy:'5', unHealthy:'10'])
            }   
        }
        stage('PMD publish Stage'){
            steps {
                step([$class: 'PmdPublisher', pattern: '**/target/pmd.xml', unstableTotalAll:'20'])	
            }   
        }
        stage('FindBug publish Stage'){
            steps {
                    step([$class: 'FindBugsPublisher', pattern: '**/findbugsXml.xml', unstableTotalAll:'20'])
            }   
        }
        stage('Deploy To Production'){
            steps {
                timeout(time:30,unit:"SECONDS"){
                input message: 'Do you approve for prod deployment?'
                }
            } 
            post{
                success{
                    echo 'Approved and code deployed to produxn now'
                }
                failure{
                    echo 'NOT Approved by QA build not deployed to produxn!'
                }
            }
        }
    }
}
