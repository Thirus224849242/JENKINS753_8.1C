pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_LOGIN = credentials('sonar-token')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube...'
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=my-app -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_LOGIN'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running OWASP Dependency-Check...'
                sh '''
                mkdir -p dependency-check
                dependency-check.sh --project my-app --scan . --format XML --out dependency-check
                '''
            }
            post {
                always {
                    publishHTML([
                        reportDir: 'dependency-check',
                        reportFiles: 'dependency-check-report.html',
                        reportName: 'Security Report'
                    ])
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                sh '''
                scp target/my-app.jar ec2-user@staging-ec2:/home/ec2-user/
                ssh ec2-user@staging-ec2 "nohup java -jar /home/ec2-user/my-app.jar > app.log 2>&1 &"
                '''
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running staging integration tests...'
                sh 'mvn verify -Pstaging-tests'
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve Deployment to Production?'
                echo 'Deploying to production server...'
                sh '''
                scp target/my-app.jar ec2-user@prod-ec2:/home/ec2-user/
                ssh ec2-user@prod-ec2 "pkill -f my-app.jar || true && nohup java -jar /home/ec2-user/my-app.jar > app.log 2>&1 &"
                '''
            }
        }
    }
}
