pipeline {
    agen none
    stages {
        stage('Build') {
            agent { docker { image 'python:3.5.1' } }
            steps {
                sh 'python --version'
                sh 'echo "Hello World"'
                sh '''
                	echo "Multiline shell steps works too"
                	ls -lah
                	echo "$(pwd)"
                '''
            }
        }
        stage('Test') {
            agent { docker { image 'python:latest' } }
            steps {
                sh 'echo "Test stage"'
                sh 'python --version'
            }
        }
        stage('Deploy') {
            agent { docker { image 'python:3.9' } }
            steps {
                sh 'echo "Deploy stage"'
                sh 'python --version'
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

