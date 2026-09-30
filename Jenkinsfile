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
        stage('Validate') {
            steps {
                sh 'test -f index.html'
                sh 'grep -qi "<html" index.html'
            }
        }
        stage('Deploy') {
            steps {
                sh 'cp index.html /var/www/html/index.html'
            }
        }
        stage('Verify') {
            steps {
                sh 'curl -sf http://localhost/ | grep -i "<title>"'
            }
        }
    }

    post {
        success { echo 'Deployment successful!' }
        failure { echo 'Pipeline failed. Check the logs.' }
    }
}
