pipeline {
    agent any

    stages {
        stage('Build & Test') {
            steps {
                bat 'echo Building the new project...'
                // Add your real build/test commands here. 
                // E.g., bat 'npm install' or bat 'python test.py'
                
                // To intentionally create a failure for Trace to catch, uncomment the next line:
                // bat 'exit 1'
            }
        }
    }

    post {
        always {
            script {
                // This sends the logs to your Trace Backend
                bat """
                curl -X POST http://localhost:8000/logs/jenkins ^
                -H "Content-Type: application/json" ^
                -d "{\\"job_name\\": \\"${env.JOB_NAME}\\", \\"build_number\\": ${env.BUILD_NUMBER}, \\"status\\": \\"${currentBuild.currentResult}\\", \\"log\\": \\"Build finished with status ${currentBuild.currentResult}\\"}"
                """
            }
        }
    }
}

