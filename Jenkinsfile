pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('cc25bcc3-a5a1-4218-b72c-745b198e535c')  // Store your GitHub token securely in Jenkins
    }

    stages {
        stage('Validation') {
            when {
                branch 'PR-*'  
            }
            steps {
                script {
                    // Code validation script (lint, tests, etc.)
                    echo 'Validando código...'
                    sh "flutter analyze"
                    // If validation fails, this will block the PR.
                    if (currentBuild.result == 'FAILURE') {
                        error('Code validation failed. PR is blocked.')
                    }
                }
            }
        }

        stage('Build & Deploy') {
            when {
                branch 'main'  // Trigger this stage only on the 'develop' branch
            }
            steps {
                script {
                    // Build and deploy logic for the 'develop' branch
                    echo 'Building and Deploying...'
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
