pipeline {

    agent none   // controller does nothing

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
                    chmod +x app/app.sh
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
                    chmod +x tests/test.sh
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
    }
}

