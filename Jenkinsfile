pipeline {
    agent any
 
    stages {
 
        stage('Build') {
            steps {
                echo 'Stage: Build'
                echo 'Tool: Maven'
                echo 'Action: Use a build automation tool to clean, compile, and package the application code.'
            }
        }
 
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage: Unit and Integration Tests'
                echo 'Tools: JUnit and TestNG'
                echo 'Action: Execute unit tests to validate individual components, and run integration tests to verify that modules interact correctly.'
            }
        }
 
        stage('Code Analysis') {
            steps {
                echo 'Stage: Code Analysis'
                echo 'Tool: SonarQube'
                echo 'Action: Perform static code analysis to ensure code quality, maintainability, and adherence to industry standards.'
            }
        }
 
        stage('Security Scan') {
            steps {
                echo 'Stage: Security Scan'
                echo 'Tool: OWASP Dependency-Check'
                echo 'Action: Conduct a security scan to detect known vulnerabilities in the project dependencies.'
            }
        }
 
        stage('Deploy to Staging') {
            steps {
                echo 'Stage: Deploy to Staging'
                echo 'Tool: AWS EC2'
                echo 'Action: Deploy the application to a staging server for validation in a controlled environment.'
            }
        }
 
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage: Integration Tests on Staging'
                echo 'Tool: TestNG'
                echo 'Action: Run integration tests in the staging environment to ensure the system behaves correctly under near-production conditions.'
            }
        }
 
        stage('Deploy to Production') {
            steps {
                echo 'Stage: Deploy to Production'
                echo 'Tool: AWS EC2'
                echo 'Action: Release the application to the production environment for end-user availability.'
            }
        }
    }
}
