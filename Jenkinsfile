pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        
        stage ('Continuous Inspection'){
          steps{
                build job: 'Continuous Inspection(SonarQube)'
            }
            post {
                success {
                    echo 'Inspection....'
                }  
            }
        }
         stage ('Nexus_Repository'){
          steps{
                build job: 'Nexus_Repository'
            }
            post {
                success {
                    echo 'Artifacts Saved....'
                }  
            }
        }
       
      stage ('Deploy to Staging){
            steps{
                timeout(time:2, unit:'DAYS'){
                    input message:'Approve Deployment?'
                }

                build job: 'Deploy-to-Staging'
            }
            post {
                success {
                    echo 'Code deployed to Staging.'
                }

                failure {
                    echo ' Deployment failed on Staging'
        
                }
   
            }
         }
  
    }
 }
