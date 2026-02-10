pipeline {
    agent none

    triggers {
        githubPush()
    }

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {

        stage('Checkout') {
            agent { label 'mac-agent' }
            steps {
                checkout scm
                sh '''
                  echo "Repository checked out"
                  echo "Branch: $(git branch --show-current)"
                '''
            }
        }

        stage('Build & Test (Parallel)') {
            parallel {

                stage('Build') {
                    agent { label 'mac-agent' }
                    steps {
                        sh '''
                          echo "===== BUILD ====="
                          chmod +x app/app.sh
                          ./app/app.sh
                        '''
                    }
                }

                stage('Test') {
                    agent { label 'node-mac1' }
                    steps {
                        sh '''
                          echo "===== TEST ====="
                          chmod +x tests/test.sh
                          ./tests/test.sh
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ PIPELINE SUCCESS'
        }
        failure {
            echo '❌ PIPELINE FAILED'
        }
    }
}

