pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Run Tests') {
            steps {
                sh '''
                    python3 -m pytest test_calculator.py -v 2>&1 | tee test-output.log
                    exit ${PIPESTATUS[0]}
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: 'test-output.log', allowEmptyArchive: true
                }
            }
        }
    }
    post {
        failure { echo 'PIPELINE FAILED - Tests did not pass' }
        success { echo 'PIPELINE PASSED - All tests green' }
    }
}
