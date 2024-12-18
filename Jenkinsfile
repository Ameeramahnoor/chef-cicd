pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Ameeramahnoor/chef-cicd.git'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: "${REPO_URL}", branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        bat '''
                            echo "Building Project..."
                            rem Example build step for Windows (you can replace it with your actual build commands)
                            rem Example: call mvn clean install for Maven build
                        '''
                    } catch (Exception e) {
                        echo "Build failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        bat '''
                            echo "Running tests..."
                            rem Example test commands for Windows (replace with your testing tools)
                            rem Example: call mvn test for Maven tests
                        '''
                    } catch (Exception e) {
                        echo "Test failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    try {
                        bat '''
                            echo "Deploying application..."
                            rem Example deployment step (replace with your deployment command)
                            rem Example: call deploy.bat
                        '''
                    } catch (Exception e) {
                        echo "Deploy failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'This will run after all stages finish.'
        }
        success {
            echo 'Build and Deployment successful!'
        }
        failure {
            echo 'Something failed during the pipeline stages.'
        }
    }
}

