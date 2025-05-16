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
                Description: Build the code using a build automation tool to compile and package
your code. You need to specify at least one build automation tool.
                Tool: Maven
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                Description: Run unit tests to ensure the code functions as
expected and run integration tests to ensure the different components of the
application work together as expected.
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
                Description:  Integrate a code analysis tool to analyse the code and ensure
it meets industry standards.
                Tool: SonarQube
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                Description: Perform a security scan on the code using a tool to identify
any vulnerabilities.
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
                Description: Deploy the application to a staging server .
                Tool: AWS EC2
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                Description: Run integration tests on the staging
environment to ensure the application functions as expected in a production-like
environment.
                Tool: JUnit
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                Description: Deploy the application to a production server.
                Tool: AWS EC2
            }
        }
    }
}
