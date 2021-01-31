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
    }
}