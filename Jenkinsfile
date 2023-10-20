pipeline {
    agent any 

    stages {
        stage('Print env') {
            steps {
                sh 'printenv'
            }
        }
        stage('Display GitHub Info') {
            steps {
                script {
                    // Check if the necessary environment variables exist (e.g., set by the GitHub plugin)
                    if (env.GIT_COMMIT) {
                        echo "Git Commit: ${env.GIT_COMMIT}"
                    }
                    
                    if (env.GIT_BRANCH) {
                        echo "Git Branch: ${env.GIT_BRANCH}"
                    }

                    if (env.GIT_URL) {
                        echo "Git URL: ${env.GIT_URL}"
                    }

                    if (env.GITHUB_EVENT_TYPE) {
                        echo "GitHub Event Type: ${env.GITHUB_EVENT_TYPE}"
                    }
                    
                    // Depending on your Jenkins and plugin setup, there might be more variables available.
                    // Add more checks here as necessary.
                }
            }
        }

        stage('Hello') {
            steps {
                echo 'Hello, World!'
            }
        }
    }
}
