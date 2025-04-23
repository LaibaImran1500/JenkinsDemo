pipeline {
    agent any

    tools {
        maven 'Maven' // Must match Jenkins tool config
    }

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Branch to build')
        string(name: 'BUILD_ENV', defaultValue: 'dev', description: 'Environment to build in (dev/stage/prod)')
    }

    environment {
        NEW_VERSION = '1.3.0'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out branch: ${params.BRANCH_NAME}"
                // SCM checkout usually happens automatically if pipeline is linked to source
            }
        }

        stage('Build') {
            steps {
                echo "Building version ${env.NEW_VERSION} on branch ${params.BRANCH_NAME}"
                //bat 'mvn clean package -Dversion=%NEW_VERSION%'
            }
        }

        stage('Unit Test') {
            when {
                expression {
                    return params.BUILD_ENV == 'dev' || params.BUILD_ENV == 'stage'
                }
            }
            steps {
                echo "Running unit tests in ${params.BUILD_ENV} environment"
                //bat 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                expression {
                    return params.BRANCH_NAME == 'main' || params.BRANCH_NAME.startsWith('release/')
                }
            }
            steps {
                echo "Deploying to ${params.BUILD_ENV} environment from branch ${params.BRANCH_NAME}"
                //bat 'echo Deploying app...'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            //deleteDir()
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
