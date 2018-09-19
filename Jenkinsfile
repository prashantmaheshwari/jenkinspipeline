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

                stage ('Deploy_to_Staging'){
                    steps {
                         build job: 'Deploy_to_Staging'
                       
                    }
               }
           }
         
        }
