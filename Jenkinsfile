pipeline {
    agent any
    tools{
        maven 'local maven'
    }
    
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
                bat '/usr/local/bin/docker build . -t tomcatwebapp:${env.BUILD_ID}'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to staging'){
            steps{
                build job: 'deploy-to-staging'
            }
        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message: 'deploy to production?'
                }
                build job: 'deploy-to-production'
            }
            post{
                success{
                    echo 'deploy success'
                }
                failure{
                    echo 'deploy failure'
                }
            }
        }
    }
}