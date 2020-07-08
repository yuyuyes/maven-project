pipeline {
    agent any
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'       
            }
        }
        post {
            success {
                echo 'starting to save'
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }  
}
