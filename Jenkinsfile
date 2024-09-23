pipeline {
    agent any
    environment {
        ARTVERSION = "${env.BUILD_ID}"
        JAVA_HOME = 'C:\\Program Files\\jdk-21.0.3' // Set to your Java 21.0.3 path
        PATH = "${env.JAVA_HOME}\\bin;${env.PATH}" // Add Java to PATH
    }
    
    stages {
        
        stage('Check Java Setup') {
            steps {
                bat 'echo JAVA_HOME is set to %JAVA_HOME%'
                bat 'java -version'
            }
        }

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
