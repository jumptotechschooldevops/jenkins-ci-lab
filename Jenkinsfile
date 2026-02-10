pipeline {
    agent none

    // ✅ Trigger on GitHub push
    triggers {
        githubPush()
    }

    options {
        timestamps()
    }

    stages {

        stage('Parallel Build & Test') {
            parallel {

                stage('Build on mac-agent') {
                    agent { label 'mac-agent' }
                    steps {
                        echo "=============================="
                        echo "BUILD STAGE"
                        echo "Node: ${env.NODE_NAME}"
                        sh '''
                            echo "Hostname: $(hostname)"
                            echo "Workspace: $(pwd)"
                            chmod +x app/app.sh
                            ./app/app.sh
                        '''
                        echo "=============================="
                    }
                }

                stage('Test on node-mac1') {
                    agent { label 'node-mac1' }
                    steps {
                        echo "=============================="
                        echo "TEST STAGE"
                        echo "Node: ${env.NODE_NAME}"
                        sh '''
                            echo "Hostname: $(hostname)"
                            echo "Workspace: $(pwd)"
                            chmod +x tests/test.sh
                            ./tests/test.sh
                        '''
                        echo "=============================="
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ PIPELINE SUCCESS (Triggered by GitHub Push)"
        }
        failure {
            echo "❌ PIPELINE FAILED"
        }
    }
}

