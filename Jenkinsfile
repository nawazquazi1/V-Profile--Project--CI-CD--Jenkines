pipeline {
    
    agent any
    environment {
        ARTVERSION = "${env.BUILD_ID}"
    }
    
    stages {
        
        stage('BUILD') {
            steps {
                bat 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('UNIT TEST') {
            steps {
                bat 'mvn test'
            }
        }

        stage('INTEGRATION TEST') {
            steps {
                bat 'mvn verify -DskipUnitTests'
            }
        }
        
        stage('CODE ANALYSIS WITH CHECKSTYLE') {
            steps {
                bat 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

    }

}
