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
     stage ('Deploy to staging'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve Deployment?'
                }

                build job: 'Deploy-to-staging'
            }
            post {
                success {
                    echo 'Code deployed to Staging.'
                }

                failure {
                    echo ' Deployment failed.'
        
                }
   
            }
        }
    }
   
 }
