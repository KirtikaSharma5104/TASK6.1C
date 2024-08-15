pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'kirtikasharma5104@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example: Use Maven to build the code
                // sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example: Run tests with a tool like JUnit or TestNG
                // sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // Example: Use a tool like SonarQube for code analysis
                // sh 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Example: Use a tool like OWASP Dependency Check
                // sh 'dependency-check.sh --project myproject --scan ./'
            }
            post {
                always {
                    emailext subject: "Jenkins: Security Scan Stage",
                              body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}",
                              to: "${EMAIL_RECIPIENT}",
                              attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example: Deploy to AWS EC2 or other staging environment
                // sh 'deploy_to_staging.sh'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example: Run integration tests on the staging server
                // sh 'run_staging_tests.sh'
            }
            post {
                always {
                    emailext subject: "Jenkins: Integration Tests on Staging",
                              body: "The Integration Tests on Staging stage has completed with status: ${currentBuild.currentResult}",
                              to: "${EMAIL_RECIPIENT}",
                              attachLog: true
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example: Deploy to production environment
                // sh 'deploy_to_production.sh'
            }
        }
    }

    post {
        always {
            emailext subject: "Jenkins: Pipeline Completed",
                      body: "The Jenkins pipeline has completed with status: ${currentBuild.currentResult}",
                      to: "${EMAIL_RECIPIENT}",
                      attachLog: true
        }
    }
}
