pipeline {
    agent any

    environment {
        STAGING_SERVER = 'ec2-user@staging-server-address'
        PRODUCTION_SERVER = 'ec2-user@production-server-address'
        EMAIL_RECIPIENT = 'divyangalokuhetti04@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example build tool: Maven
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example test automation tools: JUnit for unit tests, TestNG for integration tests
                sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Example code analysis tool: SonarQube
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example security scan tool: OWASP Dependency Check
                sh 'dependency-check --project MyProject --scan /path/to/project'
            }
            post {
                always {
                    echo 'Sending security scan email...'
                    mail to: "${env.EMAIL_RECIPIENT}",
                         subject: "Security Scan Status: ${currentBuild.currentResult}",
                         body: "The security scan stage has finished with status: ${currentBuild.currentResult}",
                         attachLog: true
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Example deployment command
                sh 'scp target/myapp.jar ${env.STAGING_SERVER}:/path/to/deploy'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Integration tests on staging
                sh 'ssh ${env.STAGING_SERVER} "java -jar /path/to/deploy/myapp.jar"'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Example deployment command
                sh 'scp target/myapp.jar ${env.PRODUCTION_SERVER}:/path/to/deploy'
            }
        }
    }
    
    post {
        always {
            echo 'Sending pipeline completion email...'
            mail to: "${env.EMAIL_RECIPIENT}",
                 subject: "Pipeline Execution Status: ${currentBuild.currentResult}",
                 body: "The pipeline has finished with status: ${currentBuild.currentResult}",
                 attachLog: true
        }
    }
}

