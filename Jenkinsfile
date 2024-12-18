pipeline {
    agent any 

    environment {
        GIT_REPO_CICD = 'https://github.com/Ameeramahnoor/chef-cicd.git'
        GIT_REPO_CHEF = 'https://github.com/Ameeramahnoor/chefrepo.git'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out the CICD repository...'
                git branch: 'main', url: "${GIT_REPO_CICD}"  // Specify the correct branch here
            }
        }

        stage('Checkout Code') {
            steps {
                echo 'Cloning Chef repository...'
                git branch: 'main', url: "${GIT_REPO_CHEF}" // Ensure the correct branch here as well
                echo 'Repository cloned successfully!'
            }
        }

        stage('Run Chef Client') {
            steps {
                echo 'Running Chef client...'
                // Replace with the commands to run Chef client, if required
                sh 'chef-client --local-mode --runlist "recipe[default]"'
            }
        }

        stage('Test Infrastructure') {
            steps {
                echo 'Testing Infrastructure...'
                // Add testing commands or scripts here
                sh './test_infrastructure.sh'
            }
        }

        stage('Deployment') {
            steps {
                echo 'Deploying application...'
                // Add your deployment steps here, e.g., deployment to a server
                sh './deploy.sh'
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs() // Cleanup after build
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check the logs!'
        }
    }
}
