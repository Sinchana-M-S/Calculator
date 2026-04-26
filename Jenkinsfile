pipeline {
    agent any

    stages {
        stage('Install') {
            steps {
                echo 'Installing dependencies...'
                sh 'echo npm install' // Simulates installing
            }
        }
        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'echo npm run build' // Simulates building
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // THIS IS WHERE YOU CAN CREATE AN ERROR LATER
                echo 'Testing Dashboard...'
                echo 'Testing Backend...'
            }
        }
    }

    post {
        always {
            script {
                // Captures the last 1000 lines of the build log
                def logText = currentBuild.rawBuild.getLog(1000).join("\n")

                // Sends everything to your Trace Dashboard
                sh """
                curl -X POST http://localhost:8000/logs/jenkins \
                -H "Content-Type: application/json" \
                -d '{
                  "job_name": "${env.JOB_NAME}",
                  "build_number": ${env.BUILD_NUMBER},
                  "status": "${currentBuild.currentResult}",
                  "log": ${groovy.json.JsonOutput.toJson(logText)}
                }'
                """
            }
        }
    }
}
