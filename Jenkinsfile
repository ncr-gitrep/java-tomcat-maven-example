pipeline {
    agent any

    stages {
        stage('Maven Build') {
            steps {
                bat 'mvn clean package'
            }
            post{
                success{
                    echo 'Archiving the project...'

                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }
        stage('Deploy the build to staging Area'){
            steps {
                build job : 'Deploy_To_Tomcat_Pipeline'
            }
        }
    }
}