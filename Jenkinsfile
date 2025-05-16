pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'
        SONAR_HOST_URL = 'http://localhost:9000'  // SonarQube server URL
        SONAR_LOGIN = credentials('sonar-token')  // Jenkins credential for SonarQube
    }

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                Description: Use Maven to clean, compile, and package the project.
                Tool: Maven
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                Description: Run JUnit-based unit and integration tests using Maven.
                Tool: JUnit
            }
            post {
                always {
                    Description: Publish JUnit test results (Surefire reports).
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                Description: Run static code analysis using SonarQube integrated with Jenkins.
                Tool: SonarQube
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                Description: Perform a security scan on project dependencies using OWASP Dependency-Check.
                Tool: OWASP Dependency-Check
            }
            post {
                always {
                    Description: Publish the generated security report in HTML format.
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                Description: Deploy the packaged application to an AWS EC2 staging instance.
                Tool: AWS EC2
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                Description: Run environment-specific integration tests on the staging server using Maven.
                Tool: JUnit
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                Description: Deploy the application to the production AWS EC2 server after manual approval.
                Tool: AWS EC2
            }
        }
    }
}
