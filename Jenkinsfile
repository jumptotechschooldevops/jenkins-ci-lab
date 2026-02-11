pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Parallel Jobs') {
            parallel {
                stage('Lint') {
                    steps {
                        echo 'Running lint'
                        sleep 3
                    }
                }

                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests'
                        sleep 5
                    }
                }

                stage('Build') {
                    steps {
                        echo 'Building application'
                        sleep 4
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}

