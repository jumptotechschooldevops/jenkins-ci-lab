pipeline {
    agent none   // Controller does NOT execute anything

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {

        stage('Build on mac-agent') {
            agent { label 'mac-agent' }
            steps {
                checkout scm
                sh '''
                    echo "=============================="
                    echo "BUILD STAGE"
                    echo "Running on host: $(hostname)"
                    echo "Workspace: $(pwd)"
                    echo "=============================="
                    ./app/app.sh
                '''
            }
        }

        stage('Test on node-mac1') {
            agent { label 'node-mac1' }
            steps {
                checkout scm
                sh '''
                    echo "=============================="
                    echo "TEST STAGE"
                    echo "Running on host: $(hostname)"
                    echo "Workspace: $(pwd)"
                    echo "=============================="
                    ./tests/test.sh
                '''
            }
        }
    }

    post {
        success {
            echo "✅ PIPELINE SUCCESS"
        }
        failure {
            echo "❌ PIPELINE FAILED"
        }
        always {
            cleanWs()
        }
    }
}

