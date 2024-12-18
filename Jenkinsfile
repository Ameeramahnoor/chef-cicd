pipeline {
    agent any  // Use any available agent (you can specify a label if needed)

    environment {
        GIT_REPO_CICD = 'https://github.com/Ameeramahnoor/chef-cicd.git'
        
        // Set up other environment variables if necessary (e.g., paths, credentials)
    }

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout CICD repository
                echo 'Checking out the CICD repository...'
                git url: "${GIT_REPO_CICD}"
            }
        }

        stage('Checkout Code') {
            steps {
                echo 'Cloning Chef repository...'
                git url: "${GIT_REPO_CHEF}"
                echo 'Repository cloned successfully!'
            }
        }

        stage('Run Chef Client') {
            steps {
                script {
                    try {
                        echo 'Running Chef client...'

                        // Ensure 'sh' is available on your system or use equivalent Windows commands if on a Windows system
                        if (isUnix()) {
                            sh 'chef-client --local-mode --runlist "recipe[myrecipe]"'  // Customize with actual runlist/commands
                        } else {
                            bat 'chef-client --local-mode --runlist "recipe[myrecipe]"'  // Use bat for Windows
                        }

                    } catch (Exception e) {
                        echo "Error during Chef client execution: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error('Failed in Chef Client execution')
                    }
                }
            }
        }

        stage('Test Infrastructure') {
            when {
                expression { return currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Running infrastructure tests...'
                // Add necessary test scripts here if needed (e.g., testing infrastructure setup after chef run)
            }
        }

        stage('Deployment') {
            when {
                expression { return currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying to target environment...'
                // Add steps for deployment like ansible, kubectl, etc.
            }
        }
    }

    post {
        always {
            // Clean workspace at the end
            echo 'Cleaning workspace...'
            cleanWs() 
        }

        success {
            echo 'Build and deployment completed successfully!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
