pipeline {
    agent any
    
    environment {
        DIRECTORY_PATH = "/path/to/code/directory"
        TESTING_ENVIRONMENT = "TestingEnv"
        PRODUCTION_ENVIRONMENT = "YourNameProductionEnv"
    }
    
    stages {
       stage('Build') {
            steps {
                echo 'Building the code using Maven'
                // Maven tool can be used for building the code
            }
        }
       stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests to ensure code functionality'
                // JUnit or TestNG can be used for unit testing
                echo 'Running integration tests to ensure component interaction'
                // Selenium or Cucumber can be used for integration testing
            }
            post {
                success {
                   
                    emailext(
                        to: 'divyangalokuhetti04@gmail.com',
                        subject: "Unit and Integration Tests: SUCCESS",
                        body: "The Unit and Integration Tests stage has succeeded.",
                        
                        attachLog: true
                    )
                }
                
            
                failure {
                   
                    emailext(
                        to: 'divyangalokuhetti04@gmail.com',
                        subject: "Unit and Integration Tests: FAILED",
                        body: "The Unit and Integration Tests stage has failed.",
                        
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code using SonarQube'
                // SonarQube can be used for code analysis
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                // OWASP ZAP can be used for security scanning
            }
            post {
                success {
                    mail to: "divyangalokuhetti04@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was succesful!"
                }
                
            
                failure {
                    mail to: "divyangalokuhetti04@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was failed!"
                }
            }
           
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging server (e.g., AWS EC2)'
                // AWS CodeDeploy or Jenkins Deploy plugin can be used for deployment
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
                // Post-deployment testing to ensure functionality in a production-like environment
            }
            post {
                success {
                    mail to: "divyangalokuhetti04@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was succesful!"
                }
                
            
                failure {
                    mail to: "divyangalokuhetti04@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was failed!"
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production server (e.g., AWS EC2)'
                // AWS CodeDeploy or Jenkins Deploy plugin can be used for deployment
            }
        }
    }
}
