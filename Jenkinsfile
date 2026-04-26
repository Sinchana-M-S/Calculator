pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'echo Building...' // Using 'bat' for Windows
            }
        }
        stage('Test') {
            steps {
                bat 'echo Testing...'
            }
        }
    }

    post {
        always {
            script {
                // This is the Windows-friendly way to send logs to Trace
                bat """
                curl -X POST http://localhost:8000/logs/jenkins ^
                -H "Content-Type: application/json" ^
                -d "{\\"job_name\\": \\"${env.JOB_NAME}\\", \\"build_number\\": ${env.BUILD_NUMBER}, \\"status\\": \\"${currentBuild.currentResult}\\", \\"log\\": \\"Build completed with status ${currentBuild.currentResult}\\"}"
                """
            }
        }
    }
}
