pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Pull the repository from GitHub
                git branch: 'main', url: 'https://github.com/Ameeramahnoor/chef-cicd.git'
            }
        }

        stage('Run Chef Client') {
            steps {
                script {
                    // Apply Chef configurations locally
                    sh 'chef-client --local-mode --runlist "recipe[my_cookbook]"'
                }
            }
        }

        stage('Test Infrastructure') {
            steps {
                script {
                    // Test infrastructure configurations with InSpec (if applicable)
                    sh 'inspec exec cookbooks/my_cookbook/tests'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deployment process initiated.'
                    // Add deployment commands if applicable
                }
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace after the pipeline completes
        }
    }
}
