pipeline {
    
    agent any
    environment {
        ARTVERSION = "${env.BUILD_ID}"
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-21' // Set your Java path here
        PATH = "${env.JAVA_HOME}\\bin;${env.PATH}" // Add Java to PATH
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
