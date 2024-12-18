pipeline {
    agent any

    environment {
        GIT_REPO_CICD = 'https://github.com/Ameeramahnoor/chef-cicd.git'
        GIT_REPO_CHEF = 'https://github.com/Ameeramahnoor/chefrepo.git'
    }

    stages {
        stage('Checkout CICD Repository') {
            steps {
                echo 'Checking out the CICD repository...'
                git url: "${GIT_REPO_CICD}"
            }
        }

        stage('Checkout Chef Repository') {
            steps {
                echo 'Cloning Chef repository...'
                git url: "${GIT_REPO_CHEF}"
            }
        }

        stage('Run Chef Client') {
            steps {
                echo 'Running Chef client...'
                powershell script: '''
                    # Run Chef client on Windows
                    Write-Host "Starting Chef client..."
                    chef-client --local-mode --runlist 'recipe[my_recipe]'
                '''
            }
        }

        stage('Test Infrastructure') {
            steps {
                echo 'Testing Infrastructure...'
                // You can replace this with any Windows-specific testing command.
                powershell script: 'Write-Host "Testing infrastructure on Windows"'
            }
        }

        stage('Deployment') {
            steps {
                echo 'Deploying application...'
                // Deployment steps for Windows, e.g., copying files, restarting services
                powershell script: '''
                    Write-Host "Deploying on Windows..."
                    # Add deployment steps like copying files, restarting services, etc.
                '''
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Cleaning workspace...'
                cleanWs()
            }
        }
    }

    post {
        failure {
            echo 'Build failed. Check the logs!'
        }
    }
}

