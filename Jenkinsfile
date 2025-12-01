pipeline {
    agent any // Designates where the entire pipeline will execute (any available agent)

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the SCM (Source Control Management) code for the project
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Starting Build...'
                // Example for a Node.js project:
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Starting Tests...'
                // Example for running tests:
                sh 'npm test'
            }
        }

        stage('Deploy') {
            when {
                // This stage will only run if the current branch is 'main'
                branch 'main'
            }
            steps {
                echo 'Starting Deployment to Production...'
                // Replace with actual deployment commands (e.g., calling an Ansible playbook,
                // using a cloud CLI, or deploying a Docker image).
                sh './deploy.sh'
            }
        }
    }

    // Post-actions that run after the entire pipeline finishes
    post {
        always {
            echo 'Pipeline finished.'
            // Clean up workspace after the build is complete
            cleanWs()
        }
        success {
            // Sends a notification if the build was successful
            echo 'Build Successful! Sending notification.'
        }
        failure {
            // Sends a notification if the build failed
            echo 'Build Failed! Review logs.'
        }
    }
}