pipeline {  // For Sonar-Jenkins Integration & React.js based code
    agent any
    tools {            // Defined tools to be used in the pipeline
      nodejs 'nodejs'
    }
    environment {                                       // Environment variables used across stages
        SONAR_PROJECT_KEY= 'Jenkins-SonarTest'          // Unique key for SonarQube project
        SONAR_SCANNER_HOME= tool 'SonarQubeScanner'     // SonarQube scanner tool path
    }
    stages {
        stage('Git Checkout') {
            steps {
                // Cloning code from GitHub using stored Jenkins credentials
                git credentialsId: "<github-credentials-id>", url: "https://github.com/<Github-Username>/Jenkins-SonarTest.git", branch: "main" // private repository
            }
        }
        stage('NPM install') {   // Installed project dependencies defined in package.json
            steps {
                sh "npm install"
            }
        }
        stage('install AJV if missing') {            // Ensuring AJV (JSON schema validator) is installed
            steps {
                sh "npm install ajv@latest --save"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: '<YourSonarToken>', variable: 'SONAR_TOKEN')]) {   // Use of Jenkins credentials (SonarQube token) securely
                        withSonarQubeEnv('SonarQube') {                                                   // Connecting to SonarQube server configured in Jenkins
                                sh '''$SONAR_SCANNER_HOME/bin/sonar-scanner \
                                -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                                -Dsonar.sources=. \
                                -Dsonar.host.url=http://<your-sonarqube-server>:9000 \
                                -DSonar.login=${SONAR_TOKEN}'''
                    }
                }
            }
        }
        stage("Quality Gate") {
            steps {
              timeout(time: 5, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        stage('Build') {                     // Build the project (disable CI=true to avoid warnings in some React apps since code was deprecated and primary purpose was integration of Sonar and Jenkins) 
            steps {
                sh "CI=false npm run build"
            }
        }
    }
}
