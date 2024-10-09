pipeline {
    agent any
    tools {
        maven 'Maven'  // Specify Maven version to use in the build
    }
    // Define parameters that can be passed to the pipeline
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Which branch to build')
        string(name: 'BUILD_ENV', defaultValue: 'dev', description: 'Which environment to build in')
    }
    // Define environment variables that can be accessed throughout the pipeline
    environment {
        NEW_VERSION = "1.3.0"
    }
    stages {
        stage('Build') {
            steps {
                echo "Building project with version: ${NEW_VERSION}"
                sh "nvm install"
            }
        }
        stage('Test') {
            when {
                expression {
                    return params.BUILD_ENV == 'dev'
                }
            }
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
    post {
        always {
            echo 'Post Build condition running'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
