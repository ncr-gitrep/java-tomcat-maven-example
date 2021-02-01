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
        stage('Deploy to prod'){
            steps{
                timeout(time:5,unit:'DAYS'){
                    input message: 'Approve Production Deployment'
                }

                build job : 'Deploy_to_prod_pipeline'
            }
            post{
                success{
                    echo 'The deployment to prod was successful'
                }
                failure{
                    echo 'The deployment to prod failed'
                }
            }
        }
    }
}