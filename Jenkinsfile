pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Example for Maven build
                    sh 'mvn clean install'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Example for running tests with Maven
                    sh 'mvn test'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    // Example using SonarQube
                    // Ensure SonarQube Scanner is installed and configured
                    sh 'mvn sonar:sonar -Dsonar.projectKey=your_project_key -Dsonar.host.url=http://your_sonarqube_url'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Example using OWASP Dependency-Check
                    sh 'dependency-check.sh --project your_project --out .'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Example deployment script using AWS CLI
                    // Make sure AWS CLI is configured with proper credentials
                    sh 'aws s3 cp your-build-artifact.zip s3://your-staging-bucket/ --region your-region'
                    // Additional deployment steps as needed
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Example using Postman collection runner
                    sh 'newman run your_postman_collection.json'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Example deployment script using AWS CLI
                    sh 'aws s3 cp your-build-artifact.zip s3://your-production-bucket/ --region your-region'
                    // Additional deployment steps as needed
                }
            }
        }
    }

    post {
        success {
            emailext(
                subject: "Build Successful",
                body: "The build was successful. Please find the build logs attached.",
                to: "kirtikasharma5104@gmail.com",
                attachmentsPattern: 'logs/**/*.log'
            )
        }
        failure {
            emailext(
                subject: "Build Failed",
                body: "The build failed. Check the logs for details.",
                to: "kirtikasharma5104@gmail.com",
                attachmentsPattern: 'logs/**/*.log'
            )
        }
    }
}
