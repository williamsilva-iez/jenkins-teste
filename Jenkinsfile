pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('jenkins')  // Store your GitHub token securely in Jenkins
    }

    stages {
        stage('Validation') {
            when {
                branch 'PR-*'  // Run this stage only for PR branches
            }
            steps {
                script {
                    // Code validation script (lint, tests, etc.)
                    echo 'Validando código...'
                    sh "flutter doctor"
                    // If validation fails, this will block the PR.
                    if (currentBuild.result == 'FAILURE') {
                        error('Code validation failed. PR is blocked.')
                    }
                }
            }
        }

        stage('Build & Deploy') {
            when {
                branch 'develop'  // Trigger this stage only on the 'develop' branch
            }
            steps {
                script {
                    // Build and deploy logic for the 'develop' branch
                    echo 'Building and Deploying...'
                    sh 'npm install'
                    sh 'npm run build'
                    // Add deploy steps here (e.g., deploy to a staging server)
                    sh 'npm run deploy'
                }
            }
        }
    }

    post {
        always {
            // Post-build actions (notifications, cleanup, etc.)
            echo 'Pipeline completed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
