pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        
        stage ('Continous Inspection'){
          steps{
                build job: 'Continuous Inspection'
            }
            post {
                success {
                    echo 'Inspection....'
                }  
            }
        }
         stage ('Nexus_Repository'){
          steps{
                build job: 'Nexus_Repo'
            }
            post {
                success {
                    echo 'Artifacts Saved....'
                }  
            }
        }
       
     stage ('Deploy to staging'){
            steps{
                 build job: 'Deploy-to-staging'
            }
            post {
                success {
                    echo 'Code deployed to Staging.'
                }

                failure {
                    echo ' Deployment failed on Staging.'
                     }  
            }
        }
        stage ('Automation testing'){
          steps{
                build job: 'Selenium_Testing'
            }
            post {
                success {
                    echo 'Testing Successfull....'
                }  
            }
        }
       
     stage ('Deploy to Production-AWS'){
            steps{
                timeout(time:2, unit:'DAYS'){
                    input message:'Approve Production Deployment?'
                }

                build job: 'Deploy-to-prod(AWS)'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed on Production.'
        
                }
   
            }
         }
  
    }
 }
