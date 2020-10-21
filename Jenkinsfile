pipeline {
    agent none
    environment { GLOBAL_ENV_VAR = 'BlueOcean' }
    stages {
        stage('Build') {
            agent { docker { image 'python:3.5.1' } }
            environment { LOCAL_ENV_VAR = '1' }
            steps {
                sh 'python --version'
                sh 'echo "Hello World"'
                sh '''
                	echo "Multiline shell steps works too"
                	ls -lah
                	echo "$(pwd)"
                '''
                sh 'echo "environment : ${GLOBAL_ENV_VAR} | ${LOCAL_ENV_VAR}"'
            }
        }
        stage('Test') {
            agent { docker { image 'python:latest' } }
            environment { LOCAL_ENV_VAR = '2' }
            steps {
                sh 'echo "Test stage"'
                sh 'python --version'
                sh 'echo "environment : ${GLOBAL_ENV_VAR} | ${LOCAL_ENV_VAR}"'
            }
        }
        stage('Deploy') {
            agent { docker { image 'python:3.9' } }
            environment { LOCAL_ENV_VAR = '3' }
            steps {
                sh 'echo "Deploy stage"'
                sh 'python --version'
                sh 'echo "environment : ${GLOBAL_ENV_VAR} | ${LOCAL_ENV_VAR}"'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
   }
}

