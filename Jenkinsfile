pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    try {
                        // Clone the Chef repository
                        echo 'Cloning the repository...'
                        git branch: 'main', url: 'https://github.com/Ameeramahnoor/chefrepo.git'
                        echo 'Repository cloned successfully!'
                    } catch (Exception e) {
                        echo "Error during code checkout: ${e.message}"
                        throw e
                    }
                }
            }
        }

        stage('Run Chef Client') {
            steps {
                script {
                    try {
                        // Run Chef client locally to apply configurations
                        echo 'Running Chef client...'
                        sh 'chef-client --local-mode --runlist "recipe[my_cookbook]"'
                        echo 'Chef client executed successfully!'
                    } catch (Exception e) {
                        echo "Error during Chef client execution: ${e.message}"
                        throw e
                    }
                }
            }
        }

        stage('Test Infrastructure') {
            steps {
                script {
                    try {
                        // Test using InSpec (for compliance testing, optional)
                        echo 'Running InSpec tests...'
                        sh 'inspec exec cookbooks/my_cookbook/tests'
                        echo 'InSpec tests passed!'
                    } catch (Exception e) {
                        echo "Error during InSpec testing: ${e.message}"
                        throw e
                    }
                }
            }
        }

        stage('Deployment') {
            steps {
                script {
                    try {
                        // Add deployment-specific tasks here (optional)
                        echo 'Starting deployment process...'
                        // Add your deployment tasks here
                        echo 'Deployment completed!'
                    } catch (Exception e) {
                        echo "Error during deployment: ${e.message}"
                        throw e
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()  // Clean the workspace after the build
            echo 'Build pipeline completed!'
        }
    }
}

